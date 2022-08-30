<template>
  <form @submit.prevent="handleSubmit">
    <label> Name :</label>
    <input type="text" v-model="name" />
    <label> Email</label>
    <input type="email" v-model="email" />
    <label> JOB </label>
    <select v-model="job">
      <option value="design">web design</option>
      <option value="ai">ai</option>
      <option value="app">app</option>
    </select>
    <label>vote for</label>
    <div>
      <input type="checkbox" value="Techmeng" v-model="names" /> techmeng
    </div>
    <div><input type="checkbox" value="Phitik" v-model="names" /> phitik</div>
    <div><input type="checkbox" value="Navin" v-model="names" />navin</div>
    <div><input type="checkbox" value="Ponlue" v-model="names" />ponlue</div>
    <label>Skill</label>
    <input type="text" v-model="skillTemp" @keyup="addSkill" />
    <div v-for="(skill, index) in skills" :key="skill" class="pill">
      <span @click="handleCut(index)">{{ skill }} </span>
    </div>
    <div>
      <input type="checkbox" v-model="term" />
      <label> Term and Condition </label>
      <div class="error" v-if="termError">{{ termError }}</div>
    </div>
    <div class="button">
      <button>submit</button>
    </div>
  </form>
</template>
<script>
export default {
  data() {
    return {
      name: "",
      email: "",
      job: "",
      term: false,
      names: [],
      skillTemp: "",
      skills: [],
      termError: "",
    };
  },
  methods: {
    addSkill(e) {
      if (e.key === "," && this.skillTemp) {
        if (!this.skills.includes(this.skillTemp)) {
          let cut = e.target.value.slice(0, -1);
          if (cut.length >= 3 && !cut.includes(",")) {
            this.skills.push(cut);
          } else {
            alert("must have 3 character");
          }
        }
        this.skillTemp = "";
      }
    },
    handleCut(index) {
      this.skills = this.skills.filter((skill, i) => {
        return i !== index;
      });
    },
    handleSubmit() {
      this.termError = !this.term ? "Please agree" : "";
      if (this.term) {
        console.log(this.name);
        console.log(this.email);
        console.log(this.job);
        console.log(this.names);
        console.log(this.skills);
      }
    },
  },
};
</script>

<style scoped>
form {
  color: #000;
  max-width: 420px;
  margin: 30px auto;
  background: rgb(245, 245, 245);
  text-align: left;
  padding: 40px;
  border-radius: 10px;
}
label {
  color: rgb(65, 65, 65);
  display: inline-block;
  margin: 25px 0 15px;
  font-size: 0.6em;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: 600;
}
input,
select {
  display: block;
  padding: 10px 6px;
  width: 100%;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid whitesmoke;
  color: rgb(71, 56, 56);
}
input[type="checkbox"] {
  display: inline-block;
  width: 16px;
  margin: 0 10px 0 0;
  position: relative;
  top: 2px;
}
.pill {
  display: inline-block;
  margin: 20px 10px 0 0;
  padding: 6px 12px;
  background: #eee;
  border-radius: 20px;
  font-size: 12px;
  letter-spacing: 1px;
  font-weight: bold;
  color: #777;
  cursor: pointer;
}
button {
  background: #0b6dff;
  border: 0;
  padding: 10px 20px;
  margin-top: 20px;
  color: white;
  border-radius: 20px;
}
.submit {
  text-align: center;
}
.error {
  color: #ff0062;
  margin-top: 10px;
  font-size: 0.8em;
  font-weight: bold;
}
</style>