<template>
  <div class="survey">
    <h1>New Member Survey</h1>
    <p>Please complete the new member survey.</p>
    <form v-on:submit.prevent="validateForm">
      <!-- v-on directive to handle the form submission. -->
      <!-- error message to be displayed when the user submits invalid form data. -->
      <p
        class="error"
        v-show="showError"
      >Please check the information you have entered. Be sure to fill in all fields.</p>

      <p>
        <label for="q1">
          Q1: How long have you been building websites?
          <br />
          <input type="text" id="q1" v-model="q1">
        </label>
      </p>
      <!-- v-model directive to this input element. -->

      <p>
        Q2: What languages interest you the most?
        <br>
        <!-- loop to duplicate the label element and structures it contains for each item in the languageOptions array. -->
        <label v-for="language in languageOptions" v-bind:key="language">
          <input type="checkbox" v-model="q2" v-bind:value="language.value">
          {{ language.text }}
          <!-- v-model directive and use v-bind:value to set the value for this checkbox. -->
          <!-- output the text to display this option to the user. -->
        </label>
      </p>

      <p>
        Q3: What other topics interest you?
        <br />
        <!-- loop to duplicate the label element and structures it contains for each item in the topicOptions array. -->
        <label v-for="topic in topicOptions" v-bind:key="topic">
          <input type="checkbox" v-model="q3" v-bind:value="topic.value">
          {{ topic.text }}
          <!-- v-model directive and use v-bind:value to set the value for this checkbox. -->
          <!-- output the text to display this option to the user. -->
        </label>
      </p>
      <p>
        <label for="q4">
          Q4: What kinds of websites would you like to build someday?
          <br />
          <textarea cols="70" rows="8" id="q4" placeholder="Type your response here." v-model="q4"></textarea>
          <!-- v-model directive on textarea. -->
        </label>
      </p>
      <p>
        <label for="q5">
          Q5: Spaces or Tabs?
          <select id="q5" v-model="q5">
            <!-- v-model directive on this select element. -->
            <option value>Select your preference.</option>
            <option value="spaces">Spaces</option>
            <option value="tabs">Tabs</option>
          </select>
        </label>
      </p>
      <p>
        <input type="submit" value="Submit" />
      </p>
    </form>
  </div>
</template>

<script>
export default {
  name: 'Survey',
  data () {
    return {
      showError: false,
      q1: '',
      q2: [],
      q3: [],
      q4: '',
      q5: '',
      languageOptions: [
        {
          text: 'JavaScript',
          value: 'js'
        },
        {
          text: 'Python',
          value: 'py'
        },
        {
          text: 'Ruby',
          value: 'ruby'
        },
        {
          text: 'Java',
          value: 'java'
        },
        {
          text: 'PHP',
          value: 'php'
        }
      ],
      topicOptions: [
        {
          text: 'Accessibility',
          value: 'axe'
        },
        {
          text: 'Experience Design',
          value: 'ux'
        },
        {
          text: 'Operations',
          value: 'ops'
        },
        {
          text: 'Search Engine Optimization',
          value: 'seo'
        },
        {
          text: 'Multimedia',
          value: 'media'
        }
      ]
    }
  },
  methods: {
    validateForm: function () {
      if ((this.q1 !== '') &&
          (this.q2.length > 0) &&
          (this.q3.length > 0) &&
          (this.q4 !== '') &&
          (this.q5 !== '')) {
        // Form is valid
        this.$router.push('secret')
      } else {
        this.showError = true
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.error {
  border: 1px solid #aa0000;
  padding: 1rem;
  color: #aa0000;
}
h1,
h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

a {
  color: #42b983;
}
</style>
