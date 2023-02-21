<template>
  <div class="table_wrapper" style="margin-right: 10px;" ref="wrapper">
    <table class="table is-responsive is-bordered is-narrow is-fullwidth" ref="table">
      <thead>
        <tr class="">
          <th style="background-color: aliceblue; font-size: small; text-align: center;" class="headcol headcol0 headrow">
            <div style="width: 80px;" >Mã PX
              <input type="text" class="input is-small input-searching" v-model="search_Mapx">
            </div>
          </th>
          <th style="background-color: aliceblue; font-size: small; text-align: center;" class="headcol headcol1 headrow">
            <div style="width: 180px;" >Lô KHPX
              <input type="text" class="input is-small input-searching" v-model="search_Lokhpx">
            </div>
          </th>
          <th style="background-color: aliceblue; font-size: small; text-align: center;" class="headcol headcol2 headrow">
            <div style="width: 150px;" >Mã SP
              <input type="text" class="input is-small input-searching" v-model="search_Masp">
            </div>
          </th>
          <th style="background-color: aliceblue; font-size: small; text-align: center;" class="headcol headcol6 headrow">
            <div style="width: 70px;" >Nhóm SP
              <input type="text" class="input is-small input-searching" v-model="search_Nhomsp">
            </div>
          </th>
          <th style="background-color: aliceblue; font-size: small; text-align: center;" class="headcol headcol3 headrow">
            <div style="width: 100px;" >Số lượng</div>
          </th>
          <th style="background-color: aliceblue; font-size: small; text-align: center;" class="headcol headcol4 headrow">
            <div style="width: 70px;" >Thời gian</div>
          </th>
          <th style="background-color: aliceblue; font-size: small; text-align: center;" class="headcol headcol5 headrow">
            <div style="width: 70px;" >Tuần</div>
          </th>
          <th style="background-color: #f3fdec; font-size: small;" v-for="week in numberOfWeeks" :key="week" class="headrow-week">
            Tuần {{ week }}
            <br>
            {{ getWeekStartDate(week) }} - {{ getWeekEndDate(week) }}
          </th>
        </tr>
      </thead>
      <tbody>
        <tr class="" v-for="dt in listData" :key="dt.id">
          <td class="headcol headcol0" style="font-size: small; background-color: #f4f2f8">{{ dt.mapx }}</td>
          <td class="headcol headcol1" style="font-size: small; background-color: #effaf5;">{{ dt.malosx }}</td>
          <td class="headcol headcol2" style="font-size: small;">{{ dt.masp }}</td>
          <td class="headcol headcol6" style="font-size: small; text-align: center;">{{ dt.nhomsp }}</td>
          <td class="headcol headcol3" style="font-size: small; text-align: center;">{{ dt.soluong }}</td>
          <td class="headcol headcol4" style="font-size: small; text-align: center;"> 1111
          </td>
          <td class="headcol headcol5" style="font-size: small; text-align: center;">{{ dt.tuan }}</td>

          <td style="font-size: small; text-align: center;" v-for="week in numberOfWeeks" :key="week">
            <template v-if="week == dt.tuan">
              {{ dt.malosx }}
            </template>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: 'YearTimeline',
  data() {
    return {
      year: 2023,
      numberOfWeeks: 52,
      months: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'],
      lokehoachpx: [],
      listData: [],
      search_Mapx: '',
      search_Lokhpx: '',
      search_Masp: '',
      search_Nhomsp: '',
      dataMockupNextPage: [
        {
          id: 31,
          mapx: "PXGC",
          malosx: 'A-BDN-81',
          masp: 'A-BDN-81',
          soluong: '2800',
          thoigian: 0.345,
          tuan: 1,

        },
        {
          id: 32,
          mapx: "PXGC1",
          malosx: 'A-BDN-81-23P1-LOSO1',
          masp: 'A-BDN-81',
          soluong: '2800',
          thoigian: 0.345,
          tuan: 2,

        },
        {
          id: 33,
          mapx: "PXGCg",
          malosx: 'A-BDN-81-23P1-LOSO1',
          masp: 'A-BDN-81',
          soluong: '2800',
          thoigian: 0.345,
          tuan: 2,

        },
        {
          id: 34,
          mapx: "PXfGC",
          malosx: 'A-BDN-81-23P1-LOSO1',
          masp: 'A-BDN-81',
          soluong: '2800',
          thoigian: 0.345,
          tuan: 2,

        },
        {
          id: 35,
          mapx: "PXGC",
          malosx: 'A-BDN-81-23P1-LOSO1',
          masp: 'A-BDN-81',
          soluong: '2800',
          thoigian: 0.345,
          tuan: 3,

        },
        {
          id: 21,
          mapx: "PXGC",
          malosx: 'A-BDN-81-23P1-LOSO1',
          masp: 'A-BDN-81',
          soluong: '2800',
          thoigian: 0.345,
          tuan: 1,

        },
        {
          id: 22,
          mapx: "PXGC",
          malosx: 'A-BDN-81-23P1-LOSO1',
          masp: 'A-BDN-81',
          soluong: '2800',
          thoigian: 0.345,
          tuan: 2,

        },
        {
          id: 23,
          mapx: "PXGC",
          malosx: 'A-BDN-81-23P1-LOSO1',
          masp: 'A-BDN-81',
          soluong: '2800',
          thoigian: 0.345,
          tuan: 2,

        },
        {
          id: 24,
          mapx: "PXGC",
          malosx: 'A-BDN-81-23P1-LOSO1',
          masp: 'A-BDN-81',
          soluong: '2800',
          thoigian: 0.345,
          tuan: 2,

        },
        {
          id: 25,
          mapx: "PXGC",
          malosx: 'A-BDN-81-23P1-LOSO1',
          masp: 'A-BDN-81',
          soluong: '2800',
          thoigian: 0.345,
          tuan: 3,

        },
      ]
    };
  },
  created() {

  },
  mounted() {
    this.showAllLokhpx();
    this.listData = this.lokehoachpx;
    this.$refs.wrapper.addEventListener('scroll', this.handleScroll);
  },
  destroyed () {
    // this.$refs.wrapper.removeEventListener('scroll', this.handleScroll);
  },
  methods: {
    getWeekStartDate(week) {
      const d = new Date(this.year, 0, 1);
      const dayOffset = d.getDay();
      const diff = (week - 1) * 7 - dayOffset;
      return new Date(this.year, 0, 1 + diff).toLocaleDateString();
    },
    getWeekEndDate(week) {
      const d = new Date(this.year, 0, 1);
      const dayOffset = d.getDay();
      const diff = (week - 1) * 7 - dayOffset;
      return new Date(this.year, 0, 1 + diff + 7).toLocaleDateString();
    },
    getWeeksInMonth(month) {
      const weeks = [];
      const d = new Date(this.year, month - 1, 1);
      const firstWeek = this.getWeekNumber(d);
      for (let i = firstWeek; i < firstWeek + 5; i++) {
        weeks.push(i);
      }
      return weeks;
    },
    getWeekNumber(date) {
      const onejan = new Date(date.getFullYear(), 0, 1);
      return Math.ceil(((date - onejan) / 86400000 + onejan.getDay() + 1) / 7);
    },

    searchData(){
      this.listData = this.lokehoachpx.filter(element => {
        let isMatchSearch = this.matchSearch(element);
        return isMatchSearch;
      });
    },
    matchSearch(element) {
      let mapx = element.mapx.toLocaleLowerCase();
      let malosx = element.malosx.toLocaleLowerCase();
      let masp = element.masp.toLocaleLowerCase();

      let isMatch1 = (this.search_Mapx && mapx.includes(this.search_Mapx.toLocaleLowerCase()) || !this.search_Mapx);
      let isMatch2 = (this.search_Lokhpx && malosx.includes(this.search_Lokhpx.toLocaleLowerCase()) || !this.search_Lokhpx)
      let isMatch3 = (this.search_Masp && masp.includes(this.search_Masp.toLocaleLowerCase())  || !this.search_Masp)

      return (isMatch1 && isMatch2 && isMatch3);
    },
    handleScroll(){
      let heightTable = this.$refs.table.offsetHeight;
      let heightWrapper = this.$refs.wrapper.offsetHeight;
      let scrollTop = this.$refs.wrapper.scrollTop;
      if(heightWrapper+scrollTop > heightTable){
        this.lokehoachpx = [...this.lokehoachpx,...this.dataMockupNextPage]
        this.listData = this.lokehoachpx;
      }
    },
    async showAllLokhpx() {
      // this.lokehoachpx = await this.$axios.$get(
      //   `/api/lokehoach/gettest`
      // );
      this.search_timestart = ""
      this.search_timeend = ""
      this.lokehoachpx = [
        {
          id: 1,
          mapx: "PXGC",
          malosx: 'A-BDN-81',
          masp: 'A-BDN-81',
          soluong: '2800',
          thoigian: 0.345,
          tuan: 1,

        },
        {
          id: 2,
          mapx: "PXGC1",
          malosx: 'A-BDN-81-23P1-LOSO1',
          masp: 'A-BDN-81',
          soluong: '2800',
          thoigian: 0.345,
          tuan: 2,

        },
        {
          id: 3,
          mapx: "PXGCg",
          malosx: 'A-BDN-81-23P1-LOSO1',
          masp: 'A-BDN-81',
          soluong: '2800',
          thoigian: 0.345,
          tuan: 2,

        },
        {
          id: 4,
          mapx: "PXfGC",
          malosx: 'A-BDN-81-23P1-LOSO1',
          masp: 'A-BDN-81',
          soluong: '2800',
          thoigian: 0.345,
          tuan: 2,

        },
        {
          id: 5,
          mapx: "PXGC",
          malosx: 'A-BDN-81-23P1-LOSO1',
          masp: 'A-BDN-81',
          soluong: '2800',
          thoigian: 0.345,
          tuan: 3,

        },
        {
          id: 11,
          mapx: "PXGC",
          malosx: 'A-BDN-81-23P1-LOSO1',
          masp: 'A-BDN-81',
          soluong: '2800',
          thoigian: 0.345,
          tuan: 1,

        },
        {
          id: 12,
          mapx: "PXGC",
          malosx: 'A-BDN-81-23P1-LOSO1',
          masp: 'A-BDN-81',
          soluong: '2800',
          thoigian: 0.345,
          tuan: 2,

        },
        {
          id: 13,
          mapx: "PXGC",
          malosx: 'A-BDN-81-23P1-LOSO1',
          masp: 'A-BDN-81',
          soluong: '2800',
          thoigian: 0.345,
          tuan: 2,

        },
        {
          id: 14,
          mapx: "PXGC",
          malosx: 'A-BDN-81-23P1-LOSO1',
          masp: 'A-BDN-81',
          soluong: '2800',
          thoigian: 0.345,
          tuan: 2,

        },
        {
          id: 15,
          mapx: "PXGC",
          malosx: 'A-BDN-81-23P1-LOSO1',
          masp: 'A-BDN-81',
          soluong: '2800',
          thoigian: 0.345,
          tuan: 3,

        },
      ]
    },
  },
  watch: {
    search_Mapx(newVal, oldVal){
      if(newVal != oldVal){
        this.searchData();
      }
    },
    search_Lokhpx(newVal, oldVal){
      if(newVal != oldVal){
        this.searchData();
      }
    },
    search_Masp(newVal, oldVal){
      if(newVal != oldVal){
        this.searchData();
      }
    },
    search_Nhomsp(newVal, oldVal){
      if(newVal != oldVal){
        this.searchData();
      }
    },

  }
};
</script>
<style scoped>
html{
  box-sizing: border-box !important;
}
.table_wrapper {
  overflow-x: scroll;
  overflow-y: scroll;
  padding: 0;
  max-height: 90vh;
  position: relative;
  background-color: lightgray;
}
table{
  background-color: lightgray;
}
table, th, td {
  border: 1px solid lightgray;
  box-sizing: border-box !important;
}

th {
  background-color: #fff;
  height: 90px;
  min-width: 52px;
  padding: 0;
}

td {
  background-color: #fff;
  min-height: 19px;
  min-width: 52px;
  height: 33px;
  padding: 0px 2px;
}

table {
  border-collapse: collapse;
}


.headcol {
  position: sticky;
  z-index: 999;
  top: auto;
  background-color: #fff;
}

.headcol0 {
  left: 0px;
  /* width: 80px; */
}

.headcol1 {
  left: 80px;
  /* width: 180px; */
}

.headcol2 {
  left: 260px;
  /* width: 150px; */
}
.headcol6 {
  left: 410px;
  /* width: 70px; */
}

.headcol3 {
  left: 480px;
  /* width: 100px; */
}

.headcol4 {
  left: 580px;
  /* width: 70px; */
}

.headcol5 {
  left: 650px;
}

.headrow{
  top: 0px;
  z-index: 9999;
}

.headrow-week{
  position: sticky;
  z-index: 999;
  top: 0px;
}

.input-searching{
  width: 85%;
  outline: none;
}

</style>
