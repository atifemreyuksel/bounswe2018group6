<template>
  <div class="dashboard-editor-container">
    <el-row>
      <router-link to="/signup">
        <el-button class="center-button" type="primary" round>Sign Me Up!</el-button>
      </router-link>
    </el-row>
    <h1 style="text-align: center"> All Events </h1>  
    <el-row>
      <el-col v-for="event in eventList" :key="event.id" :xs="{span: 24}" :sm="{span: 12}" :md="{span: 12}" :lg="{span: 6}" :xl="{span: 6}" style="margin-bottom:30px;">
        <box-card
          :event-name="event.title"
          :event-link="'events/show-event/' + event.id"
          :description="event.description"
          :date="beautifyDate(event.date)"
          :owner="event.owner.username"
          :followers="event.followers"
          :votes="event.votes"
          :price="event.price"
          :image="event.featured_image" />
      </el-col>
    </el-row>

  </div>
</template>

<script>
import BoxCard from '@/views/dashboard/admin/components/BoxCard'
import { fetchEvents } from '@/api/event'

export default {
  name: 'DashboardAdmin',
  components: {
    BoxCard
  },
  data() {
    return {
      eventList: null
    }
  },
  created() {
    this.fetchData()
  },
  methods: {
    fetchData() {
      fetchEvents().then(response => {
        this.eventList = response.data
        console.log(this.eventList)
      })
    },
    beautifyDate(date) {
      var d = new Date(date)
      date = (d.getDate()<10?'0':'') + d.getDate() + "/" + d.getMonth() + "/" + d.getFullYear() + " - " + (d.getHours()<10?'0':'')+  d.getHours() + ":" + (d.getMinutes()<10?'0':'') + d.getMinutes()
      return date
    }
  }
}
</script>

<style rel="stylesheet/scss" lang="scss" scoped>
.dashboard-editor-container {
  padding: 32px;
  background-color: rgb(240, 242, 245);
  .chart-wrapper {
    background: #fff;
    padding: 16px 16px 0;
    margin-bottom: 32px;
  }
}
.center-button{
  display:block;
  margin:auto;
}
</style>
