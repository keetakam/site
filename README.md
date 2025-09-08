สรุปการ deploy บน Azure Static Web Apps

1) ข้อกำหนดเบื้องต้น
- ตั้ง secret ใน GitHub repository ชื่อ: AZURE_STATIC_WEB_APPS_API_TOKEN
- Workflow ถูกกำหนดให้ทำงานเมื่อ push ไปยังสาขา: main (เปลี่ยนได้ใน .github/workflows)

2) คำสั่งพื้นฐาน (ท้องถิ่น)
- ติดตั้ง dependences: npm ci
- สร้าง build: npm run build
- จำลองบนเครื่อง: ติดตั้ง CLI -> npm i -g @azure/static-web-apps-cli
  แล้วรัน: swa start build --api api

3) GitHub Actions
- Workflow อยู่ที่: .github/workflows/azure-static-web-apps.yml
- Workflow จะตรวจหาโฟลเดอร์แอป (root, app, client, frontend, website) และโฟลเดอร์ api
- Workflow จะตรวจหาเอาต์พุต build เป็น build/ หรือ dist/ และคัดลอก staticwebapp.config.json เข้าไปก่อน deploy

4) การตรวจสอบเมื่อเกิดปัญหา
- ตรวจ package.json ว่ามีสคริปต์ "build"
- ถ้าเอาต์พุตไม่ถูกสร้าง ให้แก้สคริปต์ build หรือปรับ workflow ให้ชี้ไปยัง output ที่ถูกต้อง
- ตรวจ secrets และชื่อสาขาใน repository settings

5) เพิ่มเติม
- ถ้าต้องการกำหนด rewrite/route เพิ่มเติม ให้แก้ staticwebapp.config.json หรือเพิ่มไฟล์ routes.json ตามความต้องการ

ติดต่อถ้าต้องการให้ผมปรับค่า app_location/api_location/output_location ให้เฉพาะเจาะจงกับโปรเจกต์ของคุณ
