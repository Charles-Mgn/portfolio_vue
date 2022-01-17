<template>
  <div id="app">

    <div id="head">
      <nav>
        <div class="home"><a href="#home">Home</a></div>
        <div class="work"><a href="#work">My work</a></div>
        <div class="about"><a href="#about">About</a></div>
        <div class="contact"><a href="#contact">Contact</a></div>
      </nav>
    </div>


    <div id="home">
      <img src="static/img/logo.png" alt="logo" id="logo">
      <h1>Hi, I'm <span class="tonic">Charles</span>.</h1>
      <div id="introduction">I like creating things 😃</div>
      <div class="tonic slash">Front-end Development</div>
      <div class="tonic slash">UX / UI Design</div>
    </div>


    <div id="work">
      <div>
        <h2 class="tonic title">{{ content.work.devTitle }}</h2>
        <div class="project-container" v-for="project in content.work.devProjects" :key="project.id">
          <a :href="project.link" target="_blank" class="project">
            <img :src="project.img" alt="project.title">
            <h3 class="sub-title">{{ project.title }}</h3>
            <div class="project-desc">
              <p>{{ project.desc1 }}</p>
              <p>{{ project.desc2 }}</p>
            </div>
          </a>
        </div>
      </div>
      <div>
        <h2 class="tonic title">{{ content.work.designTitle }}</h2>
        <div class="project-container" v-for="project in content.work.designProjects" :key="project.id">
          <a :href="project.link" target="_blank" class="project">
            <img :src="project.img" alt="project.title">
            <h3 class="sub-title">{{ project.title }}</h3>
            <div class="project-desc">
              <p>{{ project.desc1 }}</p>
              <p>{{ project.desc2 }}</p>
            </div>
          </a>
        </div>
      </div>
      <div id="resume"><a href="assets/CV_MANGIN-Charles.pdf" download class="tonic">> Download my resume</a></div>
    </div>


    <div id="about">
      <div>
        <h2 class="tonic title">{{ content.about.who.title }}</h2>
        <div class="paragraph">{{ content.about.who.txt1 }}</div>
        <div class="paragraph">{{ content.about.who.txt2 }}</div>
      </div>

      <div id="picture">
        <div id="charles"></div>
        <div id="legend" class="tonic">Doing the things I love, while trying to better the world around me.</div>
      </div>

      <div>
        <h2 class="tonic title">{{ content.about.what.title }}</h2>
        <div class="paragraph">{{ content.about.what.txt1 }}</div>
        <div class="paragraph">{{ content.about.what.txt2 }}</div>
        <h3 class="tonic sub-title">{{ content.about.what.multimedia.title }}</h3>
        <ul>
          <li v-for="item in content.about.what.multimedia.list" :key="item.id"></li>
        </ul>

        <h3 class="tonic sub-title">{{ content.about.what.managementLaw.title }}</h3>
        <ul>
          <li v-for="item in content.about.what.managementLaw.list" :key="item.id"></li>
        </ul>
      </div>

      <div>
        <h2 class="tonic title">{{ content.about.tools.title }}</h2>
        <div class="tools">
          <h3 class="tonic sub-title">{{ content.about.tools.programming.title }}</h3>
          <ul>
            <li v-for="item in content.about.tools.programming.list" :key="item.id"></li>
          </ul>
        </div>
        <div class="tools">
          <h3 class="tonic sub-title">{{ content.about.tools.softwares.title }}</h3>
          <ul>
            <li v-for="item in content.about.tools.softwares.list" :key="item.id"></li>
          </ul>
        </div>
      </div>
    </div>

    <div id="contact">
      <h2 class="tonic title">{{ content.about.contact.title }}</h2>
      <div>
        <div class="social"><a href="https://www.linkedin.com/in/charles-m-9014a4151/" target="_blank"><i class="fab fa-linkedin"></i>LinkedIn</a></div>
        <div class="social"><a href="mailto:charlesmangin.98@gmail.com" target="_blank"><i class="fas fa-at"></i>Gmail</a></div>
        <div class="social"><a href="https://github.com/Ezellix" target="_blank"><i class="fab fa-github"></i>GitHub</a></div>
        <div class="social"><a href="https://www.instagram.com/charles_0229/" target="_blank"><i class="fab fa-instagram"></i>Instagram</a></div>
      </div>
    </div>

    <div id="more"><p>(More projects and updates coming very soon!)</p></div>

    <div id="footer">© 2022 Copyright: charlesmangin.fr</div>

  </div>
</template>

<script>
export default {
  name: 'App',
  data () {
    return {
      content: {
      }
    }
  },

  created () {
    axios.get('static/content.json').then(function (response) {
      console.log(response.data);
      this.content = response.data;
    }.bind(this))
      .catch(function (error) {
        console.log(error);
      });

    window.addEventListener('scroll', this.scrollPercentage);
  },

  destroyed () {
    window.removeEventListener('scroll', this.scrollPercentage);
  },

  methods: {
    scrollPercentage () {
      let scroll = (document.documentElement.scrollTop + document.body.scrollTop) / (document.documentElement.scrollHeight - document.documentElement.clientHeight) * 100;
      if (scroll > 95) {
        document.querySelector('.contact').classList.add("active");
        document.querySelector('.about').classList.remove("active");
        document.querySelector('.work').classList.remove("active");
        document.querySelector('.home').classList.remove("active");
      }
      else if (scroll > 50 && scroll <= 95) {
        document.querySelector('.about').classList.add("active");
        document.querySelector('.contact').classList.remove("active");
        document.querySelector('.work').classList.remove("active");
        document.querySelector('.home').classList.remove("active");
      }
      else if (scroll > 20 && scroll <= 50) {
        document.querySelector('.work').classList.add("active");
        document.querySelector('.about').classList.remove("active");
        document.querySelector('.contact').classList.remove("active");
        document.querySelector('.home').classList.remove("active");
      } else {
        document.querySelector('.home').classList.add("active");
        document.querySelector('.about').classList.remove("active");
        document.querySelector('.work').classList.remove("active");
        document.querySelector('.contact').classList.remove("active");
      }
    },
  }
}
</script>

<style>
  @import './assets/styles/style.css';
</style>
