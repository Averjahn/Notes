<template>
<div class="wrapper">
    <div id="wrapper-content">

      <section>
        <div class="container">

        <message v-if="message" :message="message" />

        <!-- <priority /> -->

        <newNote :note="note" @addNote="addNote"/>

        <div class="note-header">
          <h1>{{ title }}</h1>

        <search :value="search" placeholder="Find your note" @search="search = $event"/>

          <div class="icons">
            <svg :class="{ active: grid }" @click="grid = true" style="cursor: pointer;" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" ><rect x="3" y="3" width="7" height="7"></rect><rect x="14" y="3" width="7" height="7"></rect><rect x="14" y="14" width="7" height="7"></rect><rect x="3" y="14" width="7" height="7"></rect></svg>
            <svg :class="{ active: !grid }" @click="grid = false" style="cursor: pointer;" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><line x1="8" y1="6" x2="21" y2="6"></line><line x1="8" y1="12" x2="21" y2="12"></line><line x1="8" y1="18" x2="21" y2="18"></line><line x1="3" y1="6" x2="3" y2="6"></line><line x1="3" y1="12" x2="3" y2="12"></line><line x1="3" y1="18" x2="3" y2="18"></line></svg>
          </div>
        </div>

        <notes :notes="notesFilter" :grid="grid" @remove="removeNote" />
      

        </div>
      </section>

    </div>
  </div>
</template>

<script>
import message from '@/components/Message.vue'
import newNote from '@/components/NewNote.vue'
import notes from '@/components/Notes.vue'
import search from '@/components/Search.vue'
// import priority from '@/components/Priority.vue'
export default {

  components: {
    message, newNote, notes, search //, priority
  },

  data () {
    return {
        title: 'Notes App',
        search: '',
        message: null,
        grid: true,
        note: {
            title: '',
            discr: '',
            priority: 1
        },
        notes: [
            {
                title: 'First Note',
                discr: 'Discription for First',
                date: new Date(Date.now()).toLocaleString(),
                priority: 1
            },
            {
                title: 'Second Note',
                discr: 'Discription for Second',
                date: new Date(Date.now()).toLocaleString(),
                priority: 1
            },
            {
                title: 'Third Note',
                discr: 'Discription for Third',
                date: new Date(Date.now()).toLocaleString(),
                priority: 1
            }

        ]
      }
  },
computed: {
  notesFilter () {
    let array = this.notes,
      search = this.search
    if(!search) return array

    search = search.trim().toLowerCase()

    array = array.filter(function (item) {
      if(item.title.toLowerCase().indexOf(search) !== -1) {
        return item
      }
    })
//Error
    return array;
  }
},
 methods: {
        addNote() {
            // console.log(this.note)
            let {title, discr, priority} = this.note
            if (title ==='') {
                this.message = "title can't be blank"
                return false
            }
            console.log(`Priority is ${this.note.priority}`)
            this.notes.push({
                title,
                discr,
                date: new Date(Date.now()).toLocaleString(),
                priority
            })
            this.message = null
            this.note.title = ''
            this.note.discr = ''
            this.note.priority = 1
        },
        removeNote (index) {
          this.notes.splice(index, 1)
        }
    }
}
</script>

<style>

</style>