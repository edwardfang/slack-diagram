<template>
  <div class="app-container">
    <el-row type="flex" justify="center">
      <el-col :span="18">
        <el-card class='box-card box1'>
          <div slot="header" class="clearfix">
            <span class="text">WordCloud</span>
          </div>
          <div>
            <mywordcloud
              :team-id="this.team_info.id"
            ></mywordcloud>
          </div>
        </el-card>
      </el-col>
    </el-row>
    <el-row type="flex" justify="center">
      <el-col :span='18'>
        <el-card class='box-card box2'>
          <div slot="header" class="clearfix">
            <span class="text">User Rank</span>
          </div>
          <div>
            <chart :height="100" :data="this.data" ></chart>
          </div>
        </el-card>
      </el-col>
    </el-col>
  </el-row>
  </div>
</template>

<script>
import Chart from './chart'
import mywordcloud from './word_cloud.vue'
import { mapGetters } from 'vuex'
import { get_user_rank } from '@/api/data_process.js'

export default {
  name: 'analysis-chat',
  components: {
    mywordcloud, Chart
  },
  computed: {
    ...mapGetters([
      'team_info'
    ])
  },
  data() {
    return {
      numbers: null,
      labels: null,
      data: null
    }
  },
  created() {
    get_user_rank(this)
  }
}

</script>

<style scoped>
.text {
  font-size: 18px;
  font-family: 'Mukta Malar', sans-serif;
  font-weight: bold;
  color:#304156;
}
</style>

