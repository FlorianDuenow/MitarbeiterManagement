<template>
  <div class="Top">
    <h5 v-if="user !== undefined">{{ user.firstname }} {{ user.lastname }}</h5>
    <h5 v-else>Neuer Mitarbeiter</h5>
  </div>
  <div class="overview" uk-grid>
    <div class="uk-width-1-4 " style="margin-left: auto; margin-right: auto">
      <div class="uk-grid uk-child-width-1-1">
        <div class="uk-card uk-card-default uk-margin-small-bottom uk-card-small uk-card-body">
          <h4>Kontaktdaten</h4>
          <div class="uk-width-1-1 uk-margin-small-bottom">
            <input class="uk-input" type="text" placholder="Vorname" :value="user?.firstname ?? undefined">
          </div>
          <div class="uk-width-1-1  uk-margin-small-bottom">
            <input class="uk-input" type="text" placholder="Nachname" :value="user?.lastname ?? ''">
          </div>
          <div class="uk-width-1-1  uk-margin-small-bottom">
            <input class="uk-input" type="email" placholder="E-Mail-Adresse" :value="user?.email ?? ''">
          </div>
          <h4>Fähigkeiten</h4>
          <div class="uk-width-1-1 uk-margin-small-bottom">
            <span @click="toggleSkill(skill)" class="uk-label uk-margin-small-right" :class="user != undefined && Object.values(userSkills).some(s => s.id === skill.id) ? 'uk-label-danger' : 'label-owen' " v-for="skill in skills" :key="skill.id">
                {{skill.name}}
              </span>
          </div>
          <button v-if="user === undefined" class="uk-button-danger uk-margin-small-bottom uk-width-1-1 uk-button" @click="$emit('save')">Mitarbeiter anlegen</button>
          <button v-else class="uk-button-danger uk-margin-small-bottom uk-width-1-1 uk-button" @click="$emit('save')">Speichern</button>
          <button class="uk-button-default uk-margin-small-bottom uk-width-1-1 uk-button" @click="$emit('cancel')">Abbrechen</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
let skills = [
  {
    id: 1,
    name: 'Vue.js',
  },
  {
    id: 2,
    name: 'React',
  },
  {
    id: 3,
    name: 'Angular',
  },
  {
    id: 4,
    name: 'TypeScript',
  },
  {
    id: 5,
    name: 'Node.js',
  },
  {
    id: 6,
    name: 'Nest.js',
  },
  {
    id: 7,
    name: 'SAPUI5',
  }

]

export default {
  props: {
    user: {
      type: Object,
      required: false,
      default: undefined
    },
    save: Function,
    cancel: Function
  },
  data() {
    return {
      skills,
      userSkills: this.user?.skills ?? []
    }
  },
  methods: {
    toggleSkill(skill){
      if (Object.values(this.userSkills).some(s => s.id === skill.id)) {
        this.userSkills.splice(Object.values(this.userSkills).map(s => s.id).indexOf(skill.id), 1)
      } else {
        this.userSkills.push(skill)
      }
    }
  }
}

</script>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
}

.header {

}

.centerPeace {
  align-content: center;

}

.button {
  width: inherit;
  height: 20px;
}

.badge {
  background-color: grey;
}
.Top {
  padding-left: 20px;
  padding-top: 20px;
}
.label-owen {
  background-color: white;
  color: #f0506e;
  border: 1px solid #f0506e;
}
</style>
