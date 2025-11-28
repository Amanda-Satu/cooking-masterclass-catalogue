<template>
  <article class="card">
    <div class="thumb" v-if="course.thumbnail">
      <img :src="course.thumbnail" :alt="course.title" />
    </div>

    <div class="card-body">
      <div class="meta">
        <h2 class="title">{{ course.title }}</h2>
        <p class="chef">By {{ course.chef }}</p>
      </div>

      <div class="info">
        <span class="level">{{ course.level }}</span>
        <span class="price">{{ formattedPrice }}</span>
      </div>

      <div class="actions">
        <button
          class="save-btn"
          :disabled="!course.available || saved"
          @click="$emit('save', course.id)"
        >
          {{ saved ? 'Saved' : (course.available ? 'Save' : 'Unavailable') }}
        </button>

        <span v-if="!course.available" class="soldout">Sold Out</span>
      </div>
    </div>
  </article>
</template>

<script>
export default {
  name: 'CourseCard',
  props: {
    course: {
      type: Object,
      required: true
    },
    savedIds: {
      type: Array,
      required: true
    }
  },
  computed: {
    saved() {
      return this.savedIds.includes(this.course.id)
    },
    formattedPrice() {
      try {
        return new Intl.NumberFormat(undefined, {
          style: 'currency',
          currency: this.course.currency || 'USD'
        }).format(this.course.price)
      } catch (e) {
        return `${this.course.currency || '$'}${this.course.price}`
      }
    }
  }
}
</script>

<style scoped>
.card{
  display:flex;
  flex-direction:column;
  border:1px solid #eee;
  border-radius:10px;
  padding:12px;
  background:white;
  box-shadow: 0 2px 6px rgba(0,0,0,0.03);
}
.thumb img{width:100%; height:160px; object-fit:cover; border-radius:8px;}
.title{font-size:1.05rem; margin:0 0 4px;}
.chef{margin:0;color:#666;}
.info{display:flex; justify-content:space-between; margin-top:8px; font-weight:600;}
.level{font-size:0.85rem; color:#333; background:#f1f5f9; padding:4px 8px; border-radius:999px;}
.price{font-size:0.95rem;}
.actions{display:flex; align-items:center; gap:10px; margin-top:12px;}
.save-btn{
  padding:8px 12px;
  border-radius:8px;
  border: none;
  cursor:pointer;
  background:#0ea5a4;
  color:white;
  font-weight:700;
}
.save-btn[disabled]{opacity:0.5; cursor:not-allowed;}
.soldout{
  background:#ffedd5;
  color:#b45309;
  padding:6px 8px;
  border-radius:8px;
  font-weight:700;
  font-size:0.9rem;
}
</style>
