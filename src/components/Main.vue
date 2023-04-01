<template>
    <div class="main-page" >    <!-- v-if="!editorialStatus"  -->
      <SideBar :data="data"/>
      <div class="details-div" v-animate-css="fadeIn">
        <div class="tools-bar">
          <eva-icon
            class="tools-bar-icon"
            style="position: absolute; cursor: pointer; animation-delay: 0.8s"
            v-animate-css="'bounceInRight'"
            name="printer-outline"
            width="18px"
            title="Print"
            height="18px"
            @click="printPage()"
            animation="pulse"
            fill="#2496f4"
          ></eva-icon>
        </div>
        <section
          id="personal-details"
          v-animate-css="'bounceInRight'"
          style="animation-delay: 1.2s"
          class="details-section"
        >
          <div class="details-header">Personal Details</div>
          <ul class="personal-details-list">
            <li class="list-item">{{data.personalDetails.fullName}}</li>
            <li class="list-item">{{data.personalDetails.email}}</li>
            <li class="list-item">{{data.personalDetails.phone}}</li>
            <li class="list-item">{{data.personalDetails.location}}</li>
          </ul>
        </section>
        <section
          id="summary"
          v-animate-css="'bounceInRight'"
          style="animation-delay: 1.6s"
          class="details-section details-section-inverted"
        >
          <div class="details-header">Summary</div>
          <p class="details-paragraph">{{data.summary}}</p>
        </section>
        <section
          id="experiences"
          v-animate-css="'bounceInRight'"
          style="animation-delay: 1.9s"
          class="details-section"
        >
          <div class="details-header">Experiences</div>
          <div
            v-for="(job, key, index) in data.experiences"
            :key="key"
          >
            <div class="main-details">
              <div class="details-title">{{job.title}}</div>
              <div class="details-subtitle">{{job.subTitle}}</div>
              <div class="date-indicator">{{job.startDate}} - {{job.endDate}}</div>
              <br>
              <p class="details-paragraph" v-if="job.details.length > 0">{{job.details}}</p>
              <ul>
                <li class="details-paragraph" v-for="task in job.tasks" :key="task">{{task}}.</li>
              </ul>
            </div>
            <div v-if="index !== Object.keys(data.experiences).length - 1" class="details-divider" />
          </div>
        </section>
        <section
          id="education"
          v-animate-css="'bounceInRight'"
          style="animation-delay: 2.2s"
          class="details-section details-section-inverted"
        >
          <div class="details-header">Education</div>
          <div
            v-for="(study, key, index) in data.education"
            :key="key"
            class="list-item"
          >
            <div class="main-details">
              <div class="details-title">{{study.title}}</div>
              <div class="details-subtitle">{{study.subTitle}}</div>
              <div class="date-indicator">{{study.startDate}} - {{study.endDate}}</div>
              <br>
              <p class="details-paragraph">{{study.details}}</p>
            </div>
            <div v-if="index !== Object.keys(data.education).length - 1" class="details-divider" />
          </div>
        </section>
        <section
          id="languages"
          v-animate-css="'bounceInRight'"
          style="animation-delay: 2.5s"
          class="details-section"
        >
          <div class="details-header">Languages</div>
          <div class="details-paragraph" v-for="lang in data.languages" :key="lang.name">
            <div class="list-item">{{lang.name}} ---> {{lang.level}}</div>
          </div>
        </section>
        <section
          id="technical-skills"
          v-animate-css="'bounceInRight'"
          style="animation-delay: 2.8s"
          class="details-section details-section-inverted"
        >
          <div class="details-header">Technical Skills</div>
          <ul class="details-paragraph">
            <li class="list-item" v-for="skill in data.technicalSkills" :key="skill">{{skill}}</li>
          </ul>
        </section>
        <section
          id="projects"
          v-animate-css="'bounceInRight'"
          style="animation-delay: 3.1s"
          class="details-section"
        >
          <span class="details-header">Projects</span>
          <ul>
            <li v-for="project in data.projects" :key="project.name">
              <h6 style="font-size: 18px;font-weight: 600" :href="project.link">{{project.name}}</h6>
              <p class="details-paragraph">{{project.description}}</p>
              <a
                v-if="project.link"
                class="project-link"
                :href="project.link"
              >See project</a>
              <a
                v-if="project.sourceCode"
                class="project-link"
                :href="project.sourceCode"
              >Source code link </a>
            </li>
          </ul>
        </section>
      </div>
      <div @click="handleScrollTop()" class="scroll-top-div">
        <eva-icon name="arrowhead-up" width="30px" height="30px" animation="pulse" fill="#ffffff"></eva-icon>
      </div>
    </div>
</template>

<script>
import SideBar from "./SideBar.vue";

export default {
  name: "Main",
  components: {
    SideBar
  },
  props: ["data"],
  data() {
    return {
      editorialStatus: true,
      slideIn: {
        classes: "slideInDown",
        delay: 800
      },
      slideOut: {
        classes: "slideOutDown",
        delay: 10
      },
      fadeIn: {
        classes: "fadeIn",
        delay: 1000
      }
    };
  },
  methods: {
    handleScrollTop() {
      window.scrollTo({
        top: 0,
        behavior: 'smooth'
      });
    },
    printPage() {
      window.print();
    }
  },

  mounted() {
    console.log('hello')
    setTimeout(() => {
      window.scrollTo({
        top: 0,
        behavior: 'smooth'
      });
    }, 500)
  }
};
</script>

<style>
[v-cloak] {
  display: none;
}
</style>
