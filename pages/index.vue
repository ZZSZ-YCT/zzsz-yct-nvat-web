<!--suppress CssUnresolvedCustomProperty -->
<template>
  <Title>英才2班导航站</Title>

    <div v-if="showAnnouncement" class="announcement">
      <h3>公告</h3>
      <p v-html="announcementText"></p>
      <button @click="closeAnnouncement" :style="{ '--primary-color': systemColor }">关闭</button>
    </div>
    <!--<div class="container"> -->
      <div class="big-projects">
        <div v-for="project in bigProjects"
             :key="project.name"
             class="project-item"
             :class="{ active: project.isActive }">
          <!--@click="toggleActive(project)"-->
          <img :src="project.icon" :alt="project.name">
          <div class="project-content">
            <h3>{{ project.name }}</h3>
            <p v-html="project.description"></p>
          </div>
          <a :href="project.url"
             class="project-link"
             :style="{ '--random-color': project.color }">
            访问项目
          </a>
        </div>
      </div>
      <div class="small-projects">
        <div v-for="project in smallProjects"
             :key="project.name"
             class="small-project-item">
          <a :href="project.url"
             :style="{ '--primary-color': project.color }"
             v-bind:download="project.download ? '' : null">
            {{ project.name }}
          </a>
        </div>
      </div>
    <!--</div>-->


</template>

<script setup>
import {ref} from 'vue'

const showAnnouncement = ref(true)
const announcementText = ref("欢迎访问英才2班导航站(这里是一个公告,以后可能会写点什么东西)<\/br><script>url(<\/script>")

/*const generateRandomColor = () => {
  const hue = Math.floor(Math.random() * 360)
  const saturation = Math.floor(Math.random() * 30 + 70)
  const lightness = Math.floor(Math.random() * 30 + 70)
  return `hsl(${hue},${saturation}%,${lightness}%)`
}*/
const generateRandomColor = () => {
  const hue = Math.floor(Math.random() * 360);
  const saturation = Math.floor(Math.random() * 50 + 50); // 提高饱和度，避免灰色
  const lightness = Math.floor(Math.random() * 30 + 30); // 降低亮度，生成较深的颜色，但避免过于接近黑色
  return `hsl(${hue},${saturation}%,${lightness}%)`;
};

const bigProjects = ref([
  {
    name: "典籍",
    url: "https://classics.shittim.art/",
    description: "经典事件展示.由mycbxzd与blackhig共同驱动",
    icon: "https://static.shittim.art/images/nav-page/zzsz-badge.webp",
    isActive: false,
    color: generateRandomColor()
  },
  {
    name: "文件站",
    url: "https://yct-file.mycbxzd.top/",
    description: "一个保存文件的地方,其实主要是图片,当然,随时都可能会炸掉",
    icon: "./alist.svg",
    isActive: false,
    color: generateRandomColor()
  }
])
const systemColor = ref(generateRandomColor())

const smallProjects = ref([
  { name: "团队GitHub地址", url: "https://github.com/ZZSZ-YCT", color: systemColor },
  { name: "ClassIsland集控配置文件", url: "Management.json", color: systemColor, download: true }
])

const closeAnnouncement = () => {
  showAnnouncement.value = false
}

/*const toggleActive = (project) => {
  for (let pjt of bigProjects) pjt.isActive = !pjt.isActive

  //project.isActive = !project.isActive
}*/
/*const toggleActive = (project) => {
  for (let pjt of bigProjects) {
    pjt.isActive = false; // 关闭所有项目
  }

  project.isActive = true; // 激活当前项目
};*/
/*onMounted(() => {
  setInterval(async () => {
    const imageUrl = backgrounds[Math.floor(Math.random() * backgrounds.length)]

    const data = await $fetch(imageUrl, {
      method: 'GET',
      responseType: 'blob',
    })

    if(data) {
      const objectUrl = URL.createObjectURL(data)
      document.getElementsByClassName('page-container')[0].style.backgroundImage = `url(${objectUrl})`
    } else {
      console.error(data)
    }
  }, 5000)
})*/
</script>

<style scoped>
/*.page-container {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  background: url('https://static.shittim.art/images/BG_AronaRoom.webp') no-repeat center center fixed;
  background-size: cover;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: Arial, sans-serif;
  color: #333;
}

.header {
  margin: 20px 0;
  font-size: 28px;
  color: #444;
  text-align: center;
  text-shadow: 1px 1px 4px rgba(0, 0, 0, 0.2);
  display: flex;
  align-items: center;
  gap: 10px;
  background: rgba(255, 255, 255, 0.9);
  padding: 10px 20px;
  border-radius: 16px;
}

.container {
  width: 90%;
  max-width: 1200px;
  max-height: 70vh;
  background: rgba(255, 255, 255, 0.9);
  border-radius: 16px;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
  padding: 20px;
  display: flex;
  gap: 20px;
  flex-wrap: wrap;
  overflow-y: auto;
}*/

.announcement {
  position: absolute;
  top: 20px;
  right: 20px;
  width: 300px;
  background: rgba(255, 255, 255, 0.9);
  padding: 15px;
  border-radius: 12px;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
  font-size: 14px;
  color: #333;
}

.announcement h3 {
  margin-bottom: 10px;
  font-size: 16px;
  color: #222;
}

.announcement button {
  display: block;
  margin: 10px auto 0;
  padding: 8px 15px;
  font-size: 14px;
  font-weight: bold;
  color: white;
  background: var(--primary-color, #87CEFA);
  border: none;
  border-radius: 8px;
  cursor: pointer;
  transition: background 0.2s;
}

.announcement button:hover {
  background: rgba(100, 149, 237, 0.9);
}

.big-projects {
  flex: 2;
}

.small-projects {
  flex: 1;
}

.project-item {
  position: relative;
  display: flex;
  align-items: flex-start;
  margin-bottom: 15px;
  border-radius: 10px;
  padding: 15px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  cursor: pointer;
  transition: transform 0.2s, box-shadow 0.2s, background-color 0.2s;
  background: rgba(255, 255, 255, 0.9);
}

.project-item:hover {
  transform: translateY(-5px);
  box-shadow: 0 6px 20px rgba(0, 0, 0, 0.15);
}

.project-item.active {
  background-color: rgba(135, 206, 250, 0.2);
}

.project-item img {
  width: 50px;
  height: 50px;
  border-radius: 8px;
  margin-right: 15px;
  object-fit: cover;
}

.project-content {
  flex: 1;
}

.project-content h3 {
  margin: 0;
  font-size: 18px;
  color: #222;
}

.project-content p {
  margin: 5px 0 0;
  font-size: 14px;
  color: #444;
}

.project-link {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  background: var(--random-color, rgba(135, 206, 250, 0.8));
  color: white;
  text-align: center;
  padding: 10px;
  border-radius: 0 0 10px 10px;
  opacity: 0;
  transform: translateY(20px);
  transition: opacity 0.3s, transform 0.3s;
  text-decoration: none;
}

.project-item:hover .project-link {
  opacity: 1;
  transform: translateY(0);
}

.small-project-item {
  margin-bottom: 15px;
  text-align: center;
}

.small-project-item a {
  display: block;
  padding: 15px;
  font-size: 16px;
  font-weight: bold;
  color: white;
  background: var(--primary-color, #87CEFA);
  border-radius: 8px;
  text-decoration: none;
  transition: background 0.2s;
}

.small-project-item a:hover {
  background: rgba(100, 149, 237, 0.9);
}

/*footer {
  margin: 20px 0;
  font-size: 14px;
  color: #666;
  text-align: center;
  background: rgba(255, 255, 255, 0.9);
  padding: 10px 20px;
  border-radius: 16px;
  user-select: none;
}*/
</style>
