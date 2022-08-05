<template>
  <div>
    <button @click="activeView = 'year'">Month</button>
    <VueCal  xsmall  :time="false"
    click-to-navigate
        :transitions="false" 
        :selected-date="selectedDate"
        :disable-views="['years','day']"
        :active-view.sync="activeView"
        :class="{'active_not_year':activeView === 'week'} "
        >
        <template v-slot:weekday-heading="item">
          <span @click="chnageNoteItem(item)" :class="classesHeadingWeekDays(item)" v-if="item.view.id === 'week'">
                      {{
                        convertDateDay(item.heading.date)
                      }}
          </span>
        </template>
        </VueCal>
        <div class="mt-3" style="margin-top:30px">
          <Note v-for="item in filterNoteItem" :noteItem="item" :key="item.id"/>
        </div>
        
  </div>
</template>

<script>
import VueCal from 'vue-cal'
import 'vue-cal/dist/vuecal.css'
import moment from 'jalali-moment'

export default {
  name: 'IndexPage',
  components: { VueCal },
  computed:{
    filterNoteItem(){
      const notItem = this.dataItems.find(item=> item.date === this.selectedDate);
      return notItem?.items || []
     },
  },
  data(){
    return {
      selectedDate:moment().format("YYYY-MM-DD"),
      dataItems:[
        {
          id:1,
          date:"2022-08-05",
          items:[
            {
              id:22,
              title:"This is test for 2022-08-05",
            },
            {
              id:33,
              title:"this is test 2 for 2022-08-05"
            }
          ]
        },
        {
          id:2,
          date:"2022-08-04",
          items:[
            {
              id:22,
              title:"This is test for 2022-08-04",
            },
            {
              id:33,
              title:"this is test 2 for 2022-08-04"
            }
          ]
        }
      ],
      activeView:"week"
    }
  },
  methods:{
    chnageNoteItem(item){
      const data = moment(item.heading.date).format('YYYY-MM-DD')
      this.selectedDate = data
    },
    classesHeadingWeekDays(item){
      const data = moment(item.heading.date).format("YYYY-MM-DD");
      return {
        'btn__active': data === this.selectedDate
      }
    },
    convertDateDay(date){
      return moment(date).format('D')
    }
  }
}
</script>
<style>
.vuecal__flex.vuecal__menu{
  display: none;
}
 .vuecal__flex.weekday-label .small{
  display: none !important;
}
.vuecal__flex.weekday-label .xsmall {
  display: none !important;
}
.vuecal__flex.weekday-label .full {
  display: block !important;
}
.active_not_year .vuecal__flex.vuecal__body{
  display: none !important;
}
.btn__active{
  background: dodgerblue;
  color: #fff;
}
</style>