<template>
  <header class="header">
    <div class="brand">
      <h1>Cooking Masterclass</h1>
      <p class="tagline">Curated workshops with expert chefs</p>
    </div>
    <div class="wishlist">
      <button class="wishlist-btn" aria-label="Wishlist">
        ❤️ Wishlist
        <span class="count" :aria-live="'polite'">{{ count }}</span>
      </button>
    </div>
  </header>
</template>

<script>
export default {
  name: 'HeaderBar',
  props: {
    count: {
      type: Number,
      required: true
    }
  }
}
</script>

<style scoped>
.header{
  display:flex;
  justify-content:space-between;
  align-items:center;
  padding:16px;
  border-bottom:1px solid rgba(0,0,0,0.06);
  background: linear-gradient(90deg,#fff,#fff);
}
.brand h1{
    margin:0;
    font-size:1.25rem;
}
.tagline{
    margin:2px 0 0;
    font-size:0.9rem;
    color:#666;
}
.wishlist-btn{
  background:transparent;
  border:1px solid #eee;
  padding:8px 12px;
  border-radius:8px;
  font-weight:600;
  display:flex;
  gap:8px;
  align-items:center;
}
.count{
  background:#ff6b6b;
  color:white;
  border-radius:999px;
  padding:2px 8px;
  font-weight:700;
}
@media (max-width:600px){
  .header{
    flex-direction:column; 
    gap:8px; align-items:flex-start;}
}
</style>
