<template>
  <header class="zbr-masthead">
    <!-- Click to edit, ESC to cancel, ENTER to save, blur to save -->
    <h1 v-if="true" class="zbr-heading" :contenteditable="isTitleBeingEdited"
        @click="editTitle" @keydown.enter="saveTitleOnEnter" @blur="saveTitle"
        @keyup.esc="cancelTitle">{{title}}</h1>

    <nav class="zbr-nav">
      <ul>
        <li class="zbr-nav-item zbr-add-row" @click="addRow">+&nbsp;Add&nbsp;row</li>
        <li v-if="hasRows" class="zbr-nav-item zbr-add-card" @click="addCard">+&nbsp;Add&nbsp;card</li>
      </ul>
    </nav>
  </header>
</template>

<script>
import EventBus from './EventBus'

export default {
  name: 'Masthead',
  props: {hasRows: Boolean, title: String},
  data () {
    return {
      isTitleBeingEdited: false
    }
  },
  methods: {
    addCard: function () {
      EventBus.$emit('masthead-add-card', true)
    },
    addRow: function () {
      EventBus.$emit('row-edit-details', 'new-row')
    },
    editTitle: function () {
      this.isTitleBeingEdited = true
      // Focus needs setTimeout https://stackoverflow.com/a/37162116
      setTimeout(() => { this.$el.querySelector('.zbr-heading').focus() }, 0)
    },
    saveTitle: function () {
      let title = this.$el.querySelector('.zbr-heading').textContent
      fetch(process.env.API_URL + '/api/board/', {
        method: 'post',
        headers: new Headers({'Content-Type': 'application/json'}),
        body: JSON.stringify({title: title})
      }).catch(function (err) {
        console.error(err)
        alert('Sorry, something went wrong\n\n' + err)
      })
      this.isTitleBeingEdited = false
    },
    cancelTitle: function () {
      this.isTitleBeingEdited = false
      this.$el.querySelector('.zbr-heading').innerHTML = this.title
    },
    saveTitleOnEnter: function (ev) {
      ev.preventDefault()
      this.saveTitle()
    },
    filterKey: function (ev) {
      if (ev.key === 'Enter') {
        ev.preventDefault()
      }
    }
  },
  mounted () {
    let self = this
    EventBus.$on('board-title-loaded', function (boardTitle) {
      console.log('masthead: title loaded')
      self.title = boardTitle
    })
    EventBus.$on('global-cancel', function () {
      console.log('masthead: cancel')
      self.cancelTitle()
    })
  }
}
</script>

<style>
  .zbr-heading {
    background-color: black;
    color: white;
    font-size: 26px;
    padding: 5px 8px 4px;
    font-weight: bold;
    display: inline-block;
    margin: 0px 0 15px;
    cursor: pointer;
  }
  .zbr-nav {
    display: inline;
    position: relative;
    top: -14px;
  }

  /** Tweak heading for mobile, to avoid nav buttons breaking onto two lines */
  @media (max-width: 400px) {
    .zbr-heading {
      font-size: 22px;
    }
    .zbr-nav {
      top: -10px;
    }
  }

  .zbr-nav ul {
    display: inline;
    padding: 0;
  }
  li.zbr-nav-item {
    display: inline;
  }
  .zbr-nav-item {
    background-color: #BBB;   /* Alternate values: #209cee, #ccc */
    padding: 4px 5px 4px 4px;
    font-size: 13px;
    cursor: pointer;
    margin-left: 3px;
    border-radius: 2px;
    color: #000;
  }
  .zbr-nav-item:hover {
    background-color: #AAA;
  }
</style>
