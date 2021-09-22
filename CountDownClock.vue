<template>
  <div>
    <v-container>
      <v-row no-gutters justify="center">
        <v-col cols="3" md="2">
          <p class="text-h3 text-md-h1 font-weight-light" :style="`color: ${numberColor}`">{{ days | two_digits }}</p>
          <p class="text-body-1" :style="`color: ${textColor}`">Days</p>
        </v-col>
        <v-col cols="3" md="2">
          <p class="text-h3 text-md-h1 font-weight-light" :style="`color: ${numberColor}`">{{ hours | two_digits }}</p>
          <p class="text-body-1" :style="`color: ${textColor}`">Hours</p>
        </v-col>
        <v-col cols="3" md="2">
          <p class="text-h3 text-md-h1 font-weight-light" :style="`color: ${numberColor}`">{{ minutes | two_digits }}</p>
          <p class="text-body-1" :style="`color: ${textColor}`">Minutes</p>
        </v-col>
        <v-col cols="3" md="2">
          <p class="text-h3 text-md-h1 font-weight-light" :style="`color: ${numberColor}`">{{ seconds | two_digits }}</p>
          <p class="text-body-1" :style="`color: ${textColor}`">Seconds</p>
        </v-col>
      </v-row>
    </v-container>  
  </div>
</template>

<script>
export default {   
  // Date prop must be in this format: "2021-09-27T09:00:00Z" to avoid browser errors.
  props: {
    date: {
      type: String
    },
    numberColor: {
      type: String,
      default: "#000"
    },
    textColor: {
      type: String,
      default: "#000"
    }
  }, 

// ~~~~~~~~~~~~~~~~~~ DATA ~~~~~~~~~~~~~~~~~~~
  data() {
    return {
      now: Math.trunc((new Date()).getTime() / 1000)
    }
  },


// ~~~~~~~~~~~~~~~~~~ PROPERTIES ~~~~~~~~~~~~~~~~~~~
  computed: {
    dateInMilliseconds() {
      return Math.trunc(Date.parse(this.date) / 1000)
    },
    seconds() {
      return (this.dateInMilliseconds - this.now) % 60;
    },
    minutes() {
      return Math.trunc((this.dateInMilliseconds - this.now) / 60) % 60;
    },
    hours() {
      return Math.trunc((this.dateInMilliseconds - this.now) / 60 / 60) % 24;
    },
    days() {
      return Math.trunc((this.dateInMilliseconds - this.now) / 60 / 60 / 24);
    }
  },

  watch: {},


// ~~~~~~~~~~~~~ HOOKS ~~~~~~~~~~~~~~~~~
  mounted() {
    window.setInterval(() => {
        this.now = Math.trunc((new Date()).getTime() / 1000);
    },1000);
  },

  updated() {},


// ~~~~~~~~~~~~~~~~~~  METHODS ~~~~~~~~~~~~~~~~~~~
  methods: {},

  filters: {
    two_digits: function (value) {
      if (value < 0) {
        return '00';
      }
      if (value.toString().length <= 1) {
        return `0${value}`;
      }
      return value;
    }
  }
};

// Copyright (c) 2021 by Sergio Peña (https://codepen.io/sergixnet/pen/QvzLEO)

// Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

// The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

// THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
</script>