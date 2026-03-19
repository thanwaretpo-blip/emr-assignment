# EMR Teaching Dashboard

##  รายละเอียดโครงงาน
โครงงานนี้เป็นส่วนหนึ่งของระบบสารสนเทศโรงพยาบาล (HIS) สำหรับใช้คัดกรองข้อมูลผู้ป่วยโรคเบาหวาน และออกแบบหน้าจอ EMR เพื่อใช้ในการเรียนการสอนสำหรับนักศึกษาแพทย์และอาจารย์แพทย์

---

##  SQL Query

คำสั่ง SQL ใช้สำหรับดึงข้อมูลผู้ป่วยที่ได้รับการวินิจฉัยเป็นโรคเบาหวาน (ICD-10: E11) โดยมีเงื่อนไขดังนี้:
- เข้ารับบริการที่คลินิกอายุรกรรม
- อยู่ในช่วงวันที่ 1 มกราคม ถึง 31 มีนาคม 2026
- เรียงข้อมูลจากวันที่ล่าสุดไปเก่าที่สุด

###  SQL ที่ใช้

```sql
SELECT 
    p.FirstName,
    p.LastName,
    v.VisitDate,
    d.ICD10_Code,
    d.Attending_Doctor
FROM Patient_Data p
JOIN Visit_Log v ON p.HN = v.HN
JOIN Diagnosis_Record d ON v.VN = d.VN
WHERE 
    d.ICD10_Code LIKE 'E11%' 
    AND v.Clinic_Name = 'คลินิกอายุรกรรม'
    AND v.VisitDate BETWEEN '2026-01-01' AND '2026-03-31'
ORDER BY v.VisitDate DESC;

การอธิบาย SQL (Detailed Explanation)

คำสั่ง SQL นี้ถูกออกแบบมาเพื่อดึงข้อมูลผู้ป่วยโรคเบาหวานจากระบบฐานข้อมูลโรงพยาบาล โดยมีการเชื่อมโยงข้อมูลจาก 3 ตารางหลัก ได้แก่ Patient_Data, Visit_Log และ Diagnosis_Record

การเชื่อมตาราง (JOIN)

ใช้ JOIN เพื่อรวมข้อมูลจากหลายตารางเข้าด้วยกัน

Patient_Data เชื่อมกับ Visit_Log ผ่าน HN (Hospital Number)

Visit_Log เชื่อมกับ Diagnosis_Record ผ่าน VN (Visit Number)

งื่อนไขการคัดกรอง (WHERE)

LIKE 'E11%' ใช้คัดกรองผู้ป่วยโรคเบาหวาน

Clinic_Name = 'คลินิกอายุรกรรม'

BETWEEN '2026-01-01' AND '2026-03-31'

การจัดเรียงข้อมูล (ORDER BY)

ใช้ ORDER BY VisitDate DESC เพื่อเรียงข้อมูลจากใหม่ไปเก่า

UI/UX Design: EMR Teaching Dashboard

หน้าจอ EMR Teaching Dashboard ถูกออกแบบเพื่อรองรับการใช้งานในห้องตรวจของโรงพยาบาลมหาวิทยาลัย โดยรองรับทั้งอาจารย์แพทย์และนักศึกษาแพทย์ในหน้าจอเดียว

โครงสร้างหน้าจอ (Layout Structure)

Patient Profile
แสดงข้อมูลสำคัญของผู้ป่วย เช่น ชื่อ อายุ HN และโรคประจำตัว

Visit Timeline
แสดงประวัติการเข้ารับบริการย้อนหลังตามลำดับเวลา

Student Medical Note
สำหรับนักศึกษาแพทย์บันทึกข้อมูลเบื้องต้น

Attending Doctor Panel
สำหรับอาจารย์แพทย์ใช้วินิจฉัยและสั่งการรักษา

Medication Alert System
แจ้งเตือนการแพ้ยาและลดความผิดพลาดในการสั่งยา

จุดเด่นของการออกแบบ

ใช้หลัก Information Hierarchy

แยกบทบาท Student และ Doctor ชัดเจน

ลดจำนวนคลิก (Minimize Clicks)

เหมาะกับการใช้งานในสถานการณ์เร่งรีบ

แนวคิดการออกแบบ (Design Concept)

การออกแบบ EMR Teaching Dashboard นี้ยึดหลัก User-Centered Design โดยเน้นความรวดเร็ว ความชัดเจน และความแม่นยำในการใช้งาน ระบบถูกออกแบบให้เป็น Single Page Dashboard เพื่อลดขั้นตอนในการเข้าถึงข้อมูล และช่วยให้แพทย์สามารถตัดสินใจได้รวดเร็วขึ้น

นอกจากนี้ยังมีการแยกส่วนการใช้งานของนักศึกษาแพทย์และอาจารย์แพทย์อย่างชัดเจน เพื่อลดความสับสน และมีระบบแจ้งเตือนการใช้ยา (Medication Alert) เพื่อช่วยลดความผิดพลาดในการรักษา
