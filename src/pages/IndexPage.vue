<template>
  <q-page padding>
    <div class="text-h4 q-mb-md">
      Version Control + Docker Demo (Quasar)
    </div>

    <q-card class="q-mb-md">
      <q-card-section>
        <div class="text-h6">Git Workflow (ตัวอย่างขั้นตอนทำงาน)</div>
        <q-list bordered separator class="q-mt-sm">
          <q-item v-for="(step, index) in gitSteps" :key="index">
            <q-item-section avatar>
              <q-badge>{{ index + 1 }}</q-badge>
            </q-item-section>
            <q-item-section>
              <q-item-label>{{ step.title }}</q-item-label>
              <q-item-label caption>{{ step.detail }}</q-item-label>
            </q-item-section>
          </q-item>
        </q-list>
      </q-card-section>
    </q-card>

    <q-card class="q-mb-md">
      <q-card-section>
        <div class="text-h6">Docker Concepts (สรุปสั้น ๆ)</div>
        <q-list bordered separator class="q-mt-sm">
          <q-item v-for="(item, index) in dockerItems" :key="index">
            <q-item-section>
              <q-item-label>{{ item.title }}</q-item-label>
              <q-item-label caption>{{ item.detail }}</q-item-label>
            </q-item-section>
          </q-item>
        </q-list>
      </q-card-section>
    </q-card>

    <q-card>
      <q-card-section>
        <div class="text-h6">Docker Quick Reference (คำสั่งที่ใช้บ่อย)</div>
        <q-list bordered separator class="q-mt-sm">
          <q-item v-for="(cmd, index) in dockerCommands" :key="index">
            <q-item-section>
              <q-item-label><code>{{ cmd.command }}</code></q-item-label>
              <q-item-label caption>{{ cmd.when }}</q-item-label>
            </q-item-section>
          </q-item>
        </q-list>
      </q-card-section>
    </q-card>
  </q-page>
</template>

<script setup>
const gitSteps = [
  {
    title: 'แก้โค้ด Quasar ใน src/',
    detail: 'เพิ่มหน้า / component ใหม่ เช่น IndexPage.vue, Layout ต่าง ๆ',
  },
  {
    title: 'ตรวจสอบสถานะไฟล์',
    detail: 'ใช้คำสั่ง `git status` ดูว่าไฟล์ไหนเปลี่ยนแปลงบ้าง',
  },
  {
    title: 'เพิ่มไฟล์เข้า staging',
    detail: 'จากรากโปรเจกต์ ใช้ git add frontend/src/pages/IndexPage.vue',
  },
  {
    title: 'สร้าง commit พร้อมข้อความแบบ Conventional Commits',
    detail: 'เช่น `feat: add Git workflow demo page`',
  },
  {
    title: 'push ขึ้น GitHub',
    detail: 'ใช้ git push -u origin feature/quasar-demo แล้วเปิด Pull Request',
  },
]

const dockerCommands = [
  {
    command: 'docker build -t my-quasar-frontend:latest -f frontend/Dockerfile ./frontend',
    when: 'ใช้เมื่อต้องการ build image จาก Dockerfile โดยระบุ build context เป็นโฟลเดอร์ frontend',
  },
  {
    command: 'docker run -d -p 8080:80 --name my-quasar-frontend-container my-quasar-frontend:latest',
    when: 'ใช้เมื่อต้องการรัน container จาก image และ map พอร์ต 8080 บนเครื่องไปยังพอร์ต 80 ใน container',
  },
  {
    command: 'docker compose up -d --build',
    when: 'ใช้เมื่อต้องการ build image และรันบริการทั้งหมดใน docker-compose.yml แบบ background',
  },
  {
    command: 'docker compose down',
    when: 'ใช้เมื่อต้องการหยุดและลบ container รวมถึง network ที่ Docker Compose สร้างขึ้น',
  },
  {
    command: 'docker ps --filter name=my-quasar-frontend-container',
    when: 'ใช้เมื่อต้องการตรวจสอบว่า container กำลังรันอยู่หรือไม่',
  },
  {
    command: 'docker compose logs frontend',
    when: 'ใช้เมื่อต้องการดู log ของบริการ frontend เพื่อตรวจสอบข้อผิดพลาดหรือสถานะการทำงาน',
  },
]

const dockerItems = [
  {
    title: 'Image',
    detail: 'แพ็กเกจที่มีไฟล์และการตั้งค่าที่ใช้สร้าง container เช่น image ที่รวม Quasar SPA กับ Nginx',
  },
  {
    title: 'Container',
    detail: 'อินสแตนซ์ที่สร้างจาก image เช่น container ที่รัน Nginx เพื่อเสิร์ฟไฟล์ Quasar',
  },
  {
    title: 'Volume',
    detail: 'เก็บข้อมูลให้คงอยู่แยกจากวงจรชีวิตของ container เช่น ไฟล์อัปโหลดของ backend',
  },
  {
    title: 'Network',
    detail: 'ให้บริการใน Docker ติดต่อกันได้ เช่น Nginx ส่งต่อคำขอไปยัง Express',
  },
]
</script>