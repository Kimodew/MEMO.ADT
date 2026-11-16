# 03. การออกแบบโครงสร้างข้อมูล (Data Schema & Taxonomy)

โครงสร้างฐานข้อมูลถูกออกแบบให้ **ยืดหยุ่นสูง (Flexible Schema)** เพื่อให้รองรับทั้งผลงานเก่าที่มีเพียงรูปภาพ และผลงานใหม่ที่มีข้อมูลเล่มรายงานครบถ้วน

---

## 1. ผังเอนทิตีหลัก (Core Entities)

```mermaid
erDiagram
    SUBMISSION_ROOM ||--o{ PROJECT : "collects"
    PROJECT ||--o{ PROJECT_MEMBER : "has"
    PROJECT ||--o{ PROJECT_MEDIA : "contains"
    PROJECT }o--|| MAJOR : "belongs to"
    PROJECT }o--o| ADVISOR : "advised by"
    PROJECT ||--o{ PROJECT_TAG : "has"
    TAG ||--o{ PROJECT_TAG : "tagged in"

    SUBMISSION_ROOM {
        string id PK
        string room_code UK "เช่น SE-2567-X9"
        string title "ชื่อห้องส่งงาน"
        string major_id FK "รหัสสาขาวิชา"
        int academic_year "ปีการศึกษา"
        string advisor_id FK "อาจารย์ที่ปรึกษาเริ่มต้น"
        datetime deadline "วันเวลาปิดรับส่ง"
        string status "active | closed"
        datetime created_at
    }

    PROJECT {
        string id PK
        string room_id FK "รหัสห้องส่งงาน (Optional - NULL สำหรับงานเก่า)"
        string edit_token UK "รหัสแก้ไขเฉพาะกลุ่ม (สำหรับ นศ. แก้งานเดิม)"
        string revision_note "ข้อความแจ้งแก้ไขจากอาจารย์ (Optional)"
        string title_th "ชื่อภาษาไทย"
        string title_en "ชื่อภาษาอังกฤษ (Optional)"
        string slug "URL slug"
        string description "คำอธิบายสั้น (Showcase summary)"
        string category "Senior Project | Coursework | Competition | Research"
        int academic_year "ปีการศึกษา เช่น 2567"
        int semester "ภาคการศึกษา 1 | 2 (Optional)"
        string major_id FK "รหัสสาขาวิชา"
        string advisor_id FK "รหัสอาจารย์ที่ปรึกษา (Optional)"
        string co_advisor "อาจารย์ที่ปรึกษาร่วม (Optional)"
        string abstract_th "บทคัดย่อไทย (Optional)"
        string abstract_en "บทคัดย่ออังกฤษ (Optional)"
        string report_file_url "ลิงก์ไฟล์เล่มรายงาน PDF (Optional)"
        string poster_file_url "ลิงก์ไฟล์โปสเตอร์ (Optional)"
        string live_demo_url "ลิงก์เว็บไซต์/แอปที่รันจริง (Optional)"
        string github_url "ลิงก์ Source Code (Optional)"
        string video_url "ลิงก์วิดีโอเดโม YouTube/Vimeo (Optional)"
        string cover_image_url "รูปภาพหน้าปกหลัก"
        boolean is_featured "ผลงานไฮไลต์หน้าแรก"
        string award_title "รางวัลที่ได้รับ (Optional)"
        string status "draft | pending | changes_requested | published"
        datetime created_at
        datetime updated_at
    }

    PROJECT_MEMBER {
        string id PK
        string project_id FK
        string student_id "รหัสนักศึกษา (Optional)"
        string full_name "ชื่อ-นามสกุล"
        string role "หน้าที่ในโปรเจกต์ เช่น Developer, 3D Artist"
        string portfolio_url "ลิงก์ Portfolio/LinkedIn (Optional)"
        string email "อีเมล (Optional)"
    }

    PROJECT_MEDIA {
        string id PK
        string project_id FK
        string media_type "image | video | webgl_embed"
        string url "URL ของสื่อ"
        string caption "คำบรรยายภาพ (Optional)"
        int sort_order "ลำดับการแสดงผล"
    }

    MAJOR {
        string id PK "รหัสประจำหลักสูตร เช่น CE-UG, SE, MTA, DTBI, DCE, CE-MS, DTT, CE-PHD"
        string code "ตัวย่อทางการ เช่น CE, DCE, SE, DTBI, MTA, DTT"
        string name_th "ชื่อสาขาวิชาภาษาไทย"
        string name_en "ชื่อสาขาวิชาภาษาอังกฤษ"
        string level "bachelor | master | doctoral"
        string degree "วศ.บ. | วท.บ. | วศ.ม. | วท.ม. | ปร.ด."
        string color_theme "โค้ดสีประจำสาขาสำหรับ UI Tag"
    }

    ADVISOR {
        string id PK
        string full_name_th "ชื่อ-นามสกุลภาษาไทย"
        string full_name_en "ชื่อ-นามสกุลภาษาอังกฤษ"
        string email "อีเมล"
        string academic_rank "ตำแหน่งทางวิชาการ เช่น อ., ผศ.ดร."
    }

    TAG {
        string id PK
        string name "เช่น React, Unity, Flutter, IoT, AI, Blender"
        string category "tool | language | domain"
    }
```

---

## 2. จุดเด่นของการออกแบบ Schema นี้

1. **ปลอดภัยต่อข้อมูลเก่า (Old Projects Safe):**
   * ฟิลด์อย่าง `report_file_url`, `abstract_th`, `abstract_en`, `advisor_id`, `student_id` ล้วนเป็น `NULLABLE (Optional)`
   * งานเก่าแม้มีแค่ `title`, `cover_image_url`, `academic_year`, `major_id` ก็สามารถบันทึกและแสดงผลเป็นการ์ดผลงานที่สวยงามได้ทันที
2. **รองรับผลงานประเภทกลุ่ม:**
   * ตาราง `PROJECT_MEMBER` แยกออกมาอย่างชัดเจน สามารถระบุสมาชิกได้ตั้งแต่ 1 คน จนถึงทีมใหญ่ พร้อมระบุหน้าที่ (Role) ของแต่ละคนในโครงงานได้
4. **รองรับระบบห้องส่งงานและโทเคนแก้ไข (Room Code & Edit Token):**
   * ตาราง `SUBMISSION_ROOM` ช่วยให้อาจารย์สร้างรหัสห้องแจกเด็กได้หลายรอบ
   * ฟิลด์ `edit_token` ใน `PROJECT` ช่วยให้นักศึกษาสามารถกลับเข้ามาแก้ไขงานของกลุ่มตนเองได้โดยไม่ต้องสร้างบัญชีผู้ใช้ซับซ้อน และไม่เกิดงานซ้ำซ้อน
   * ฟิลด์ `room_id` เป็น `NULLABLE` เพื่อรองรับการที่อาจารย์หรือแอดมินเพิ่มงานเก่าเข้าสู่ระบบโดยตรง (Direct Add) โดยไม่ต้องผ่านห้องส่งงาน
     ```sql
     -- ตัวอย่างการดึงข้อมูลเพื่อสรุป AUN-QA แยกตามสาขา (CE, DCE, SE, DTBI, MTA, DTT)
     SELECT major_id, academic_year, COUNT(id) AS total_projects 
     FROM projects 
     WHERE category = 'Senior Project' AND status = 'published'
     GROUP BY major_id, academic_year;
     ```
