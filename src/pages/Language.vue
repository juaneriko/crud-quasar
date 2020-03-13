<template>
  <q-page class="bg-grey-3 column">
    <div class="row q-pa-sm bg-primary">
        <q-input
          class="col"
          square
          filled
          bg-color="white"
          v-model="newLanguage"
          @keyup.enter="addLanguage"
          label="Add Language"
          dense>
        <template v-slot:append>
          <q-btn
            @click="addLanguage"
            round
            dense
            flat
            icon="add" />
        </template>
      </q-input>
    </div>
    <q-list
    class="bg-white"
    separator
    border>
      <q-item
        v-for="(language, index) in languages"
        :key="language.title"
        @click="language.done = !language.done"
        :class="{'done' : language.done}"
        clickable
        v-ripple>
        <q-item-section  avatar>
          <q-checkbox
          v-model="language.done"
          class="no-pointer-events"
          color="primary" />
        </q-item-section>
        <q-item-section>
          <q-item-label>{{language.title}}</q-item-label>
        </q-item-section>
        <q-item-section
        v-if="language.done"
        side>
         <q-btn
           @click.stop="deleteLanguage(index)"
           round
           dense
           color="primary"
           icon="delete"
           />
           </q-item-section>
      </q-item>

    </q-list>
    <div
      v-if="!languages.length"
      class="no-language absolute-center">
        <q-icon
          name="check"
          size="100px"
          color="primary" />
        <div class="text-h5 text-primary text-center">
            No Language
        </div>
    </div>
  </q-page>
</template>

<script>
export default {
  data () {
    return {
      newLanguage: '',
      languages: [
        // {
        //   title: 'English',
        //   done: false
        // },
        // {
        //   title: 'Mandarin',
        //   done: true
        // },
        // {
        //   title: 'Tagalog',
        //   done: false
        // }
      ]
    }
  },
  methods: {
    deleteLanguage (index) {
      this.$q.dialog({
        title: 'Confirm',
        message: 'You sure you want to delete?',
        cancel: true,
        persistent: true
      }).onOk(() => {
        this.languages.splice(index, 1)
        this.$q.notify('Language Deleted')
      })
    },
    addLanguage () {
      this.languages.push({
        title: this.newLanguage,
        done: false

      })
      this.newLanguage = ''
    }
  }
}
</script>

<style lang="scss">
.done {
    .q-item__label {
        text-decoration: line-through;
        color: #bbb;
    }
}

.no-language {
    opacity: 0.5;
}

</style>
