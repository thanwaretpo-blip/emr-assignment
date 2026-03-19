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

