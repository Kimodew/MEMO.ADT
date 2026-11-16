# 📚 สารบัญและภาพรวมเอกสารการวางแผน (MEMO.ADT Master Planning Index)

โครงการพัฒนาระบบคลังผลงานคัดสรรและจัดแสดงนวัตกรรมดิจิทัล  
**สำนักวิชาเทคโนโลยีดิจิทัลประยุกต์ มหาวิทยาลัยแม่ฟ้าหลวง (School of Applied Digital Technology - ADT MFU)**

---

## 📑 สรุปสารบัญเอกสารการวางแผนทั้งหมด

| รหัสเอกสาร | ชื่อเอกสาร | สาระสำคัญ |
| :---: | :--- | :--- |
| ⭐ **00** | [00-master-draft-v1-baseline-spec.md](file:///e:/web/MEMO.ADT/Planning/00-master-draft-v1-baseline-spec.md) | **[เอกสารดราฟต์ฉบับอ้างอิงมาตรฐานเวอร์ชันแรก (v1.0 Baseline Draft)]**<br>• สรุปสเปกและกฎเหล็ก UI/UX ที่สร้างเสร็จสมบูรณ์ในระบบปัจจุบัน 100%<br>• กฎการตัดแคปซูล/ข้อความยัดไส้, ผัง Header Desktop/Mobile, สเปกฟอร์ม 5 ส่วน, I18n และ Admin Suite |
| **01** | [01-project-concept-and-strategy.md](file:///e:/web/MEMO.ADT/Planning/01-project-concept-and-strategy.md) | • โมเดล Hybrid (Showcase เป็นหลัก ประดับด้วยคลังวิชาการ)<br>• ขอบเขตเป็น "คลังผลงานคัดสรรถาวร" (Curated Archive) ไม่พึ่งพา Google Drive<br>• จำแนก 4 สิทธิ์ผู้ใช้งาน (Viewers, Contributors, Reviewers, Admins) |
| **02** | [02-features-and-user-stories.md](file:///e:/web/MEMO.ADT/Planning/02-features-and-user-stories.md) | • ฟังก์ชันหน้า Showcase ค้นหา/กรอง (CE, DCE, SE, DTBI, MTA, DTT)<br>• ระบบห้องส่งงาน (Room Code System) ให้อาจารย์สร้างโค้ดแจกเด็ก<br>• กลไกแก้ผลงาน 2 ทาง (อาจารย์แก้เองโดยตรง หรือส่งกลับให้เด็กแก้งานเดิมผ่าน Edit Token)<br>• ปุ่ม Direct Add สำหรับนำเข้างานเก่าย้อนหลัง |
| **03** | [03-data-schema-design.md](file:///e:/web/MEMO.ADT/Planning/03-data-schema-design.md) | • โครงสร้างฐานข้อมูล ER Diagram รองรับ MySQL 100%<br>• ออกแบบฟิลด์เล่มรายงาน/บทคัดย่อเป็น Nullable เพื่อปลอดภัยต่องานเก่า<br>• ตาราง Submission Rooms, Projects, Members, Media, Majors |
| **04** | [04-tech-stack-and-architecture.md](file:///e:/web/MEMO.ADT/Planning/04-tech-stack-and-architecture.md) | • สถาปัตยกรรมสำหรับ Server มหาวิทยาลัยแม่ฟ้าหลวง<br>• **Backend & Framework:** Laravel (PHP 8.2+) + MySQL / MariaDB<br>• **Frontend:** Blade Templates + Tailwind CSS + Alpine.js<br>• **Storage:** Local Disk Storage บน Server มหาวิทยาลัย ป้องกันไฟล์สูญหาย |
| **05** | [05-study-programmes-taxonomy.md](file:///e:/web/MEMO.ADT/Planning/05-study-programmes-taxonomy.md) | • หลักสูตรและตัวย่อทางการของ ADT: **CE, DCE, SE, DTBI, MTA, DTT**<br>• ชุดสีอัตลักษณ์ไทยโทนทางการประจำแต่ละสาขาวิชา (เขียวตอง, พวงอังกาบ, เมฆสนธยา, แดงตัด, ดินแดงตัด, น้ำเงิน ADT) |
| **06** | [06-brand-identity-and-ui-guidelines.md](file:///e:/web/MEMO.ADT/Planning/06-brand-identity-and-ui-guidelines.md) | • อ้างอิงจากคู่มือ CI ทางการ (`CI_ADT.pdf`)<br>• ชุดสีหลัก: สีน้ำเงิน `#061C90`, สีฟ้าดิจิทัล `#1CA4E1`, สีดำ `#050505`<br>• ตารางรหัสสีไทยโทนทางการประจำสาขาวิชา |
| **07** | [07-ui-design-system-spec.md](file:///e:/web/MEMO.ADT/Planning/07-ui-design-system-spec.md) | • สเปกดีไซน์สไตล์ **Shopify Editorial Frameless x YouTube Ghost Hover Capsule**<br>• ระบบข้อมูล 4 มุมบนภาพหน้าปก (ป้ายสาขาเรืองแสง, รางวัลสีทอง, ไอคอนสื่อ 4 ชนิดแนวนอน, ป้ายยอดวิว)<br>• แสง Hover Capsule สีประจำสาขาแบบบางเบา (Faint Thai Tone Tint 6–8%)<br>• ปุ่มและตัวกรองทรงแคปซูลมนกลมเต็มรูป (`rounded-full`) |
| **08** | [08-responsive-and-mobile-strategy.md](file:///e:/web/MEMO.ADT/Planning/08-responsive-and-mobile-strategy.md) | • กลยุทธ์ **Mobile-First Experience 100%** สำหรับหน้า Showcase<br>• แถบตัวกรองรูดเลื่อนแนวนอนด้วยนิ้วโป้ง (Horizontal Swipeable Pills)<br>• การ์ดผลงานเรียง 1 คอลัมน์เต็มจอ เลื่อนฟีดดูเพลินเหมือน Behance/IG<br>• ขยายเป็น 3 คอลัมน์เมื่อเปิดบนจอคอมพิวเตอร์ |
| **CI** | `CI_ADT.pdf` | เอกสารคู่มืออัตลักษณ์ทางการของสำนักวิชา ADT ฉบับสมบูรณ์ |
