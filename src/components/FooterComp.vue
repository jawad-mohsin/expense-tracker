<template>
  <footer>
    <div class="footer-container">
      <div class="copyright">
        &copy; 2024 Jawad Mohsin. All Rights Reserved.
      </div>
      <div class="social-links">
        <a href="mailto:jawadmohsin1147@gmail.com" target="_blank"
          ><i class="fa fa-envelope"></i
        ></a>
        <a href="https://www.linkedin.com/in/jawadmohsin/" target="_blank"
          ><i class="fa-brands fa-linkedin"></i
        ></a>
        <a href="https://github.com/jawad-mohsin" target="_blank"
          ><i class="fa fa-github"></i
        ></a>
        <a href="https://www.instagram.com/jawad.mohsinn/" target="_blank"
          ><i class="fa fa-instagram"></i
        ></a>
      </div>
      <div class="designed-by">Created by ~ JD</div>
    </div>
  </footer>
</template>

<script>
export default {
  name: "FooterComp",
};
</script>

<style scoped>
footer {
  background-color: #333;
  padding: 20px;
  text-align: center;
  position: fixed;
  bottom: 0%;
  width: 100%;
  z-index: 100; /* Places the footer on top of other content */
}

.footer-container {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  height: 100%;
}

.copyright,
.designed-by {
  font-size: 14px;
  color: #fff;
}

.designed-by {
  margin-top: 10px;
}

.social-links {
  display: flex;
  justify-content: space-around;
  margin-top: 10px;
}

.social-links a {
  color: #fff;
  font-size: 20px;
  margin: 0 10px;
  text-decoration: none;
}

.social-links a:hover {
  color: #493b92;
}

.fa {
  font-size: 20px;
}

@media (max-width: 768px) {
  .footer-container {
    flex-direction: row;
    justify-content: space-between;
  }

  .copyright,
  .designed-by {
    text-align: left;
  }
}
</style>
