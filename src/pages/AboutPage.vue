<template>
  <div class="about-page">
    <div class="box">
      <div class="about-section">
        <h1 class="about-title">About Us</h1>
        <div class="about-description">
          <p>
            We are two students passionate about cooking and technology. Our goal
            is to provide food enthusiasts with a platform to discover and explore
            delicious recipes from around the world.
          </p>
          <p>
            This web app utilizes the Spoonacular API, which allows us to fetch a
            wide variety of recipes and provide users with personalized search
            options based on their dietary preferences and restrictions.
          </p>
          <p>
            Through this project, we aim to make cooking more accessible and
            enjoyable for everyone, whether you're a beginner or an experienced
            chef. We hope you find inspiration and delight in the culinary journey
            we've created.
          </p>
        </div>
      </div>
      <div class="developers-section">
        <h2 class="developers-title">Meet the Developers</h2>
        <div class="developer">
          <div class="developer-image">
            <img src="path-to-student1-image.jpg" alt="Student 1">
          </div>
          <div class="developer-info">
            <h3 class="developer-name">Student 1</h3>
            <p class="developer-description">
              Lorem ipsum dolor sit amet, consectetur adipiscing elit. Integer
              ultrices, neque in aliquam posuere, ipsum lorem mattis nisi.
            </p>
          </div>
        </div>
        <div class="developer">
          <div class="developer-image">
            <img src="path-to-student2-image.jpg" alt="Student 2">
          </div>
          <div class="developer-info">
            <h3 class="developer-name">Student 2</h3>
            <p class="developer-description">
              Lorem ipsum dolor sit amet, consectetur adipiscing elit. Integer
              ultrices, neque in aliquam posuere, ipsum lorem mattis nisi.
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "AboutPage",
};
</script>

<style scoped>
.about-page {
  margin: 2rem;
}

.box {
  border: 1px solid #ccc;
  border-radius: 8px;
  padding: 2rem;
  background: linear-gradient(
    to right,
    rgba(255, 255, 255, 0.1),
    rgba(141, 184, 133, 0.1),
    rgba(99, 158, 88, 0.1)
  );
  border-radius: 10px;
  width: 80%;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.3);
}

.about-title {
  font-size: 2rem;
  font-weight: bold;
  margin-bottom: 1rem;
}

.about-description {
  line-height: 1.5;
}

.developers-title {
  font-size: 1.5rem;
  font-weight: bold;
  margin-bottom: 1rem;
}

.developer {
  display: flex;
  align-items: center;
  margin-bottom: 1rem;
}

.developer-image {
  width: 80px;
  height: 80px;
  border-radius: 50%;
  overflow: hidden;
  margin-right: 1rem;
}

.developer-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.developer-info {
  flex-grow: 1;
}

.developer-name {
  font-size: 1.2rem;
  font-weight: bold;
  margin-bottom: 0.5rem;
}

.developer-description {
  line-height: 1.5;
}
</style>
