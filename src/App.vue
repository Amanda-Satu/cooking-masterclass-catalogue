<template>
  <div id="app" class="container">
    <HeaderBar :count="wishlist.length" />

    <main>
      <section class="controls">
        <div class="intro">
          <h2>Explore Courses</h2>
          <p>Browse workshops hosted by expert chefs. Save what interests you.</p>
        </div>
        <div class="filters">
          <label>
            <input type="checkbox" v-model="filterAvailable" />
            Show only available
          </label>
        </div>
      </section>

      <section class="grid">
        <CourseCard
          v-for="c in filteredCourses"
          :key="c.id"
          :course="c"
          :savedIds="wishlist"
          @save="handleSave"
        />
      </section>

      <footer class="note">
        <small>Prototype catalogue — no login or checkout (client request)</small>
      </footer>
    </main>
  </div>
</template>

<script>
import HeaderBar from './components/HeaderBar.vue'
import CourseCard from './components/CourseCard.vue'
import coursesData from './data/courses.js'

export default {
  name: 'App',
  components: { HeaderBar, CourseCard },
  data() {
    return {
      courses: coursesData,
      wishlist: [],
      filterAvailable: false
    }
  },
  computed: {
    filteredCourses() {
      if (this.filterAvailable) {
        return this.courses.filter(c => c.available)
      }
      return this.courses
    }
  },
  methods: {
    handleSave(courseId) {
      if (!this.wishlist.includes(courseId)) {
        this.wishlist.push(courseId)
      }
    }
  }
}
</script>

<style>
/* Basic global layout */
:root{
  --bg:#fbfbfd;
  --muted:#6b7280;
  --accent:#0ea5a4;
}
body{
  font-family:Inter,system-ui,-apple-system,"Segoe UI",Roboto,"Helvetica Neue",Arial;
  background:var(--bg);margin:0;color:#111
}
.container{
  max-width:1100px;
  margin:24px auto;
  padding:0 16px;
}
main{
  margin-top:16px;
}
.controls{
  display:flex;
  justify-content:space-between;
  align-items:center;gap:12px;
  margin-bottom:16px;
}
.intro h2{
  margin:0;
}
.intro p{
  margin:6px 0 0;
  color:var(--muted)}
.grid{
  display:grid;
  grid-template-columns: repeat(3, 1fr);
  gap:16px;
}
.note{
  margin-top:18px;
  color:var(--muted);
   text-align:center}

/* Responsive */
@media (max-width:900px){
  .grid{grid-template-columns: repeat(2, 1fr);}
}
@media (max-width:600px){
  .grid{grid-template-columns: 1fr;}
  .controls{flex-direction:column;align-items:flex-start}
}
</style>
