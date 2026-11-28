<template>
  <q-page padding>
    <div class="text-h4 q-mb-md">Version Control + Docker Demo (Quasar)</div>
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
        <div class="text-h6">Docker Quick Reference</div>
        <div class="text-caption text-grey-7">คำสั่ง Docker / Docker Compose ที่ใช้บ่อย</div>
        <q-list bordered separator class="q-mt-sm">
          <q-item v-for="cmd in dockerCommands" :key="cmd.command">
            <q-item-section avatar>
              <q-icon name="terminal" color="primary" />
            </q-item-section>
            <q-item-section>
              <q-item-label class="text-mono">{{ cmd.command }}</q-item-label>
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
  { title: 'แก้โค้ด Quasar ใน src/', detail: 'เพิ่มหน้า / component ใหม่ เช่น IndexPage.vue, Layout ต่าง ๆ' },
  { title: 'ตรวจสอบสถานะไฟล์', detail: 'ใช้คำสั่ง `git status` ดูว่าไฟล์ไหนเปลี่ยนแปลงบ้าง' },
  { title: 'เพิ่มไฟล์เข้า staging', detail: 'ใช้ `git add .` หรือ `git add src/pages/IndexPage.vue`' },
  { title: 'สร้าง commit พร้อมข้อความแบบ Conventional Commits', detail: 'เช่น `feat: add Git workflow demo page`' },
  { title: 'push ขึ้น GitHub', detail: 'ใช้ `git push origin feature/quasar-demo` แล้วเปิด Pull Request' },
]

const dockerItems = [
  { title: 'Image', detail: 'แม่พิมพ์ของ container สร้างจาก Dockerfile เช่น image สำหรับ Quasar SPA' },
  { title: 'Container', detail: 'instance ของ image ที่กำลังรัน เช่น container ที่รัน Nginx เสิร์ฟไฟล์ของ Quasar' },
  { title: 'Volume', detail: 'ใช้เก็บข้อมูลถาวร เช่น log / ไฟล์ upload (frontend อาจไม่ใช้มากเท่า backend)' },
  { title: 'Network', detail: 'เชื่อม container ระหว่างกัน เช่น frontend คุยกับ backend ผ่าน network ของ Docker' },
]

const dockerCommands = [
  { command: 'docker compose up -d --build', when: 'ใช้เมื่อเริ่มรันโปรเจกต์ หรือหลังแก้โค้ด เพื่อ build image ใหม่และรันทุก service แบบเบื้องหลัง' },
  { command: 'docker compose ps', when: 'ใช้เมื่ออยากเช็กว่า container ของแต่ละ service กำลังรันอยู่หรือไม่ และเปิด port อะไรไว้' },
  { command: 'docker compose logs -f frontend', when: 'ใช้เมื่อแอปมีปัญหา เพื่อดู log ของ service frontend แบบสด ๆ' },
  { command: 'docker compose exec frontend sh', when: 'ใช้เมื่อต้องการเข้าไปพิมพ์คำสั่งข้างใน container เช่น ตรวจไฟล์หรือ environment' },
  { command: 'docker compose down', when: 'ใช้เมื่อเลิกใช้งาน เพื่อหยุดและลบ container กับ network ที่ compose สร้างไว้' },
  { command: 'docker images', when: 'ใช้เมื่ออยากดูรายการ image ที่มีในเครื่อง และขนาดของแต่ละ image' },
]
</script>

<style scoped>
.text-mono {
  font-family: monospace;
}
</style>
