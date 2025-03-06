<template>
  <div class="newsroom-container">
    <div v-for="news in newsList" :key="news.id" class="news-item">

      <div class="news-image-container">
        <img :src="getImageUrl(news.image_url)" class="news-image" alt="News Image" />
        <div class="date-badge">
          <span class="day">{{ formatDate(news.created_at).day }}</span>
          <span class="month">{{ formatDate(news.created_at).month }}</span>
        </div>

      </div>

      <div class="share-container">
        <button class="btn btn-link share-btn">
          <i class="bi bi-share-fill"></i> SHARE
        </button>
      </div>
      <hr>
      <div class="news-content">
        <p class="author">{{ getAuthor(news.author_id) }}</p>
        <h2 class="title">{{ news.title }}</h2>
        <p class="description">{{ news.body }}</p>
        <a href="#" class="read-more">READ ARTICLE</a>
      </div>
    </div>

    <div class="pagination">
      <button v-for="n in 10" :key="n" class="page-btn" :class="{ active: n === 11 }">{{ n }}</button>
    </div>
  </div>
</template>

<script>
  import newsData from "../data/news.json";
  import authors from "../data/authors.json";

  export default {
    data() {
      return {
        newsList: newsData,
      };
    },
    methods: {
      getAuthor(authorId) {
        const author = authors.find(a => a.id === authorId);
        return author ? author.name : 'Unknown';
      },
      getImageUrl(imageFileName) {
        return new URL(`/src/assets/${imageFileName}`, import.meta.url).href;
      },
      formatDate(dateString) {
        const date = new Date(dateString);
        const options = { day: '2-digit', month: 'short' };
        const formatted = date.toLocaleDateString('en-US', options).split(' ');
        return { day: formatted[1], month: formatted[0].toUpperCase() };
      },
    },
  };
</script>

<style scoped>
  .newsroom-container {
    max-width: 1000px;
    margin: auto;
    font-family: Arial, sans-serif;
  }

  .news-item {
    background: white;
    border-radius: 8px;
    overflow: hidden;
    margin-bottom: 30px;
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  }

  .news-image-container {
    position: relative;
  }

  .news-image {
    width: 100%;
    height: auto;
    border-bottom: 3px solid #ddd;
  }

  .date-badge {
    position: absolute;
    bottom: -10px;
    left: 20px;
    background: red;
    color: white;
    padding: 8px;
    border-radius: 5px;
    font-weight: bold;
    text-align: center;
  }

  .date-badge .day {
    display: block;
    font-size: 18px;
  }

  .date-badge .month {
    font-size: 12px;
  }

  .share-container {
    display: flex;
    justify-content: flex-end;
    padding: 10px 20px;
  }

  .share-btn {
    font-size: 14px;
    color: black;
    font-weight: bold;
    text-decoration: none;
  }

  .share-btn i {
    margin-right: 5px;
  }

  .news-content {
    padding: 20px;
  }

  .author {
    color: red;
    font-weight: bold;
    margin-bottom: 5px;
  }

  .title {
    font-size: 20px;
    font-weight: bold;
    margin-bottom: 10px;
  }

  .description {
    color: #555;
    font-size: 14px;
    margin-bottom: 15px;
  }

  .read-more {
    font-weight: bold;
    text-decoration: none;
    color: black;
  }

  .pagination {
    display: flex;
    justify-content: center;
    margin-top: 20px;
  }

  .page-btn {
    background: #fff;
    border: 1px solid #ddd;
    padding: 5px 10px;
    margin: 0 3px;
    cursor: pointer;
  }

  .page-btn.active {
    background: red;
    color: white;
    font-weight: bold;
  }
</style>
