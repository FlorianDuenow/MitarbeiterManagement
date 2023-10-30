<template>
  <div v-if="!showCreateUser">
    <div class="Top">
      <h5 class="Top">Mitarbeiterübersicht</h5>
    </div>
    <div class="overview" uk-grid>
      <div class="uk-width-1-4 " style="margin-left: auto; margin-right: auto">
        <div class="uk-grid uk-child-width-1-1">
          <button class="uk-button-danger uk-margin-small-bottom uk-width-1-1 uk-button" @click="showCreateUser=true">
            Mitarbeiter Anlegen
          </button>
          <div class="uk-card uk-card-default uk-margin-small-bottom uk-card-small uk-card-body" v-for="user in users"
               :key="user.id">
            <div class="uk-width-1-1 uk-text-large">
              <div class="uk-grid">
                <div class="uk-width-5-6 ">
                  {{ user.firstname }} {{ user.lastname }}
                </div>
                <div class="uk-width-1-6 ">
                  <span class="uk-text-right" @click="showEdit(user.id)" uk-icon="icon:pencil"></span>
                </div>
              </div>
            </div>
            <div class="uk-width-1-1">
              {{ user.email }}
            </div>
            <div class="uk-width-1-1">
               <span class="uk-label uk-label-danger uk-margin-small-right" v-for="skill in user.skills" :key="skill.id">
                  {{ skill.name }}
                </span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
  <CreateEmployee v-if="showCreateUser" :user="selectedUser" @save="showCreateUser = false" @cancel="showCreateUser=false"/>


</template>
<script>
import CreateEmployee from './CreateEmployee.vue'

let users = [
  {
    id: 1,
    firstname: 'Max',
    lastname: 'Mustermann',
    email: 'test@test.de',
    skills: [{
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
    ]
  },
  {
    id: 2,
    firstname: 'Mickey',
    lastname: 'Maus',
    email: 'test@test.de',
    skills: [{
      id: 1,
      name: 'Vue.js',
    },
      {
        id: 5,
        name: 'Node.js',
      },
    ]
  }

]
let showCreateUser = false;
let selectedUser = undefined;
export default {
  components: {
    CreateEmployee
  },
  data() {
    return {
      showCreateUser,
      users,
      selectedUser
    }
  },
  methods: {
    showEdit(userId) {
      this.showCreateUser = true;
      this.selectedUser = Object.values(users).filter(u => u.id === userId)[0];
    }
  }
}


</script>


<style scoped>
.Top {
  padding-left: 20px;
  padding-top: 20px;
}

.overview {
  align-content: center;
}

</style>