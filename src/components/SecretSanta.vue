<template>
  <div class="secretsanta">
    <h1>{{ msg }}</h1>
    <div v-for="(email, index) in emails" :key="'input-' + index">
      <input v-model="email.value" type="email" v-on:keydown.tab="addEmail" ref="email" />
    </div>
    <button @click="addEmail">Add Email (Tab for next)</button>
    <h2>Emails</h2>
    <div v-for="(email, index) in emails" :key="'list-' + index">
      {{ email.value }}
    </div>
    <button @click="scrambleEmails">Scramble Emails</button>    
    <button @click="clear">Clear</button>
    <br />
    <div class="pre-formatted">{{ result }}</div>
    <!--<button @click="sendEmails">Send Emails</button>-->
  </div>
</template>

<script>
export default {
  name: "SecretSanta",
  data: () => ({
    emails: [{}],
    scrambledEmails: new Map(),
    result: "",
  }),
  methods: {
    addEmail: function () {
      this.emails.push({ value: "" });
      this.$refs['input-0'].focus();
    },
    scrambleEmails: function () {
      const emailSize = this.emails.length;
      const targetEmails = [...this.emails];
      if (emailSize > 1) {
        for (let currentEmail of this.emails) {
          let targetEmail = currentEmail;
          while (currentEmail == targetEmail) {
            const index = Math.floor(Math.random() * targetEmails.length);
            targetEmail = targetEmails[index];
          }

          this.scrambledEmails.set(currentEmail.value, targetEmail.value);
          const indexToRemove = targetEmails.indexOf(targetEmail);
          targetEmails.splice(indexToRemove, 1);
          targetEmail = null;
        }
        this.scrambledEmails.forEach((value, key) => {
          this.result += key + " is giving a present to " + value + "!\n";
        });
      }
    },
    clear: function () {
      this.emails = [];
      this.scrambledEmails.clear();
      this.result = "";
    },
  },
  props: {
    msg: String,
  },
};
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
  color: #42b983;
}
.pre-formatted {
  white-space: pre;
}
</style>
