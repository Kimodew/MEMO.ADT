# 07. ข้อกำหนดระบบการออกแบบ UI สไตล์ Shopify x ADT (Design System Specification)

อ้างอิงจากระบบการออกแบบสไตล์ **Shopify High-Contrast Editorial & Cinematic System** ผสานกับ **Brand CI ของสำนักวิชา ADT**:

---

## 1. ปรัชญาการออกแบบ (Design Philosophy)
* **Monochrome First:** ดำสนิท (`#000000`) และขาวบริสุทธิ์ (`#FFFFFF`) เป็นแกนหลัก ตัดด้วยเฉดสีเทา Zinc (`#18181B` ถึง `#F4F4F5`)
* **Big Type is Light, Small Type is Firm:** ตัวหนังสือหัวข้อใหญ่ใช้ฟอนต์บางเบา (Weight 300–350) พร้อมบีบระยะห่างชิดกัน (Tight Tracking) ส่วนตัวหนังสือขนาดเล็กหรือป้ายกำกับใช้ความหนาชัดเจน (Weight 500–550)
* **Full Pill Geometry:** ปุ่ม Action และตัวกรอง (Filter) ทุกชิ้นใช้ทรงแคปซูลมนสมบูรณ์ (`rounded-full` 9999px) สลับสีพื้นขาว-ดำ (Inversion)
* **ADT Digital Accent:** สีฟ้าดิจิทัลของสำนักวิชา ADT (`#1CA4E1`) ใช้เป็นสีเน้น (Selective Accent) เฉพาะจุดสำคัญ เช่น แสงเรืองตอน Hover, ป้ายสาขาวิชา และสถานะของระบบ

---

## 2. โทนสีและโทเค็น (Color Tokens)

```css
:root {
  /* Canvas & Surfaces */
  --bg-primary: #000000;         /* พื้นหลังหลักดำสนิท */
  --bg-surface: #0E0E10;         /* พื้นผิวการ์ดและพาเนล */
  --bg-surface-elevated: #18181B;/* พื้นผิวป๊อปอัป / Modal */

  /* Hairlines & Borders */
  --border-subtle: #27272A;      /* เส้นขอบบาง 1px ประจำการ์ด */
  --border-strong: #3F3F46;      /* เส้นขอบควบคุมเมื่อโฟกัส */

  /* Text & Inks */
  --text-primary: #FFFFFF;        /* ตัวหนังสือหลัก ขาวคมชัด 100% */
  --text-muted: #A1A1AA;          /* ตัวหนังสือรอง / คำอธิบาย สบายตา */
  --text-dim: #71717A;            /* ข้อความกำกับส่วนย่อย */

  /* ADT Signature Accents */
  --adt-cyan: #1CA4E1;           /* ฟ้าดิจิทัล ADT สำหรับ Hover & Active */
  --adt-blue: #061C90;           /* น้ำเงินเข้ม ADT สำหรับ Header / Brand */
  --adt-glow: rgba(28, 164, 255, 0.25); /* แสงเรืองรอบการ์ดเมื่อชี้ */
}
```

---

## 3. สไตล์ชิ้นส่วนหน้าจอ (Component Recipes)

### 3.1 ปุ่มกดทรงแคปซูล (Pill Buttons)
* **Primary Button:** พื้นหลัง `#FFFFFF` ตัวหนังสือ `#000000` มนกลม `rounded-full` ขนาดความสูง 44px (หรือ 56px ใน Mobile) เมื่อชี้เปลี่ยนเป็นสี `#D4D4D8`
* **Secondary / Outline Button:** พื้นโปร่งใส ขอบขาวบาง 1.5px ตัวหนังสือสีขาว เมื่อชี้ขอบจะสว่างขึ้น
* **Filter Tag Pill:** แคปซูลขนาดเล็กสำหรับเลือกสาขา (CE, DCE, SE, DTBI, MTA, DTT) เลื่อนปัดซ้าย-ขวาบนมือถือได้สะดวก

### 3.2 การ์ดแสดงผลงาน (Shopify Editorial Frameless Card x YouTube Ghost Hover Capsule)
การ์ดผลงานที่ผ่านการปรับจูนจนได้รูปแบบที่ลงตัวสูงสุด:

* **โครงสร้างการ์ด (Card Geometry):**
  * ไร้กรอบสี่เหลี่ยมทึบตัน (Frameless Editorial) ในสภาวะปกติ (Rest State)
  * เว้นระยะขอบรอบทิศทาง `-m-3.5 p-3.5 rounded-3xl`
  * เมื่อเมาส์ชี้ (Hover State): ปรากฏแคปซูลแก้วดำใส สไตล์ YouTube Hover Capsule (`hover:bg-zinc-900/80 hover:shadow-2xl hover:-translate-y-1`) พร้อมเส้นขอบเรืองแสงสีประจำสาขาแบบบางเบาสบายตา (Faint Thai Tone Tint 6–8%)
  * ตัวหนังสือชื่อเรื่องยังคงเป็นสีขาวบริสุทธิ์ (`text-white`) คมชัด และลูกศร `→` สไลด์ขวาเบาๆ

* **ระบบป้าย 4 มุมบนภาพหน้าปก (4-Corner Information Geometry):**
  1. **มุมซ้ายบน (Top-Left):** ป้ายตัวย่อสาขา (`CE`, `SE`, `MTA`, `DTBI`, `DCE`, `DTT`) แคปซูลแก้วดำใส `bg-black/80 backdrop-blur-md` พร้อม **จุดกลมเรืองแสงสีไทยโทนแท้** และขอบย้อมสีโปร่งแสง
  2. **มุมขวาบน (Top-Right):** ป้ายเกียรติยศ / รางวัล (`Award Badge`) โทนสีทองแอมเบอร์ `#F59E0B`
  3. **มุมซ้ายล่าง (Bottom-Left):** แถวไอคอนสื่อที่เข้าถึงได้ภายในโครงงาน (`Media Capabilities`) เรียงแนวนอนในวงกลมแก้วดำใสขนาด 24×24px (`h-6 w-6`):
     * 📖 **สมุด**: มีเอกสารรูปเล่มโครงงานฉบับสมบูรณ์ (PDF/Report)
     * 🎬 **แคลปเปอร์บอร์ด**: มีคลิปวิดีโอสาธิตผลงาน (Video Demo)
     * 🎮 **จอยเกม**: มีระบบทดลองเล่น / WebGL Interactive 3D
     * 💻 **คอมพิวเตอร์**: มีซอร์สโค้ด GitHub ให้ศึกษา
  4. **มุมขวาล่าง (Bottom-Right):** แคปซูลแสดงจำนวนผู้เข้าชม (`View Count Pill`) ไอคอนรูปตา `👁` พร้อมตัวเลขยอดวิว (เช่น `396`, `868`, `1.2k`) แก้วดำใสขอบบาง สบายตา ไม่บดบังภาพหลัก
