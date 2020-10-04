<template>
  <div class="detail">
    <template v-if="isloaded">
      <div class="photo">
        <img class="photo-container" :src="imageUrl[0]">
        <div class="photo-layer"></div>
        <div class="photo-info">
          <div class="photo-infoInside">
            <p class="font font-h1 fontC-primary">{{today|currency}}<span class="font-h3">/1晚</span></p>
            <div class="btn btn-primary" @click.prevent="modalShow = true">Booking now</div>
          </div>
        </div>
      </div>
      <div class="description">
        <div class="description-title">
          <p class="font font-display2 fontC-primary">{{roomDetail.name}}</p>
          <p class="font font-h7 fontC-primary">
            <span>{{filterGuest}}人．</span>
            <span>{{bedKind}}床．</span>
            <span v-if="roomDetail.amenities.Breakfast === true">附早餐．</span>
            <span>衛浴{{roomDetail.descriptionShort['Private-Bath']}}間．</span>
            <span>{{roomDetail.descriptionShort.Footage}}平方公尺</span>
          </p>
        </div>
        <div class="description-content">
          <p class="font font-h7 fontC-primary">
            <span>平日（一~四）價格：{{roomDetail.normalDayPrice|currency}}／</span>
            <span>假日（五~日）價格：{{roomDetail.holidayPrice|currency}}</span>
          </p>
          <p class="font font-h7 fontC-primary">
            <span>入住時間：{{roomDetail.checkInAndOut.checkInEarly}}（最早）／</span>
            <span>{{roomDetail.checkInAndOut.checkInLate}}（最晚）</span>
          </p>
          <p class="font font-h7 fontC-primary">退房時間：{{roomDetail.checkInAndOut.checkOut}}</p>
        </div>
        <div class="rules">
          <p class="font font-h7 fontC-primary" v-if="roomDetail.descriptionShort.Bed[0] === 'Single'">．單人間僅供一位客人使用</p>
          <p class="font font-h7 fontC-primary">．臥室配有{{bedKind}}床和私人浴室</p>
          <p class="font font-h7 fontC-primary">．您需要的一切為您準備：床單和毯子，毛巾，肥皂盒洗髮水，吹風機。</p>
          <p class="font font-h7 fontC-primary">．房間裡有AC，當然還有WiFi。</p>
        </div>
        <div class="amenities">
          <div class="amenities-icon">
            <img src="@/assets/image/surface1.png" alt="" v-if="roomDetail.amenities.Breakfast === true" class="icon">
            <img src="@/assets/image/surface1.png" alt="" v-else style="opacity: 0.2;" class="icon">
            <img src="@/assets/image/correct.png" alt="" class="mark" v-if="roomDetail.amenities.Breakfast === true">
            <img src="@/assets/image/false.png" alt="" class="mark" v-else style="opacity: 0.2;">
          </div>
          <div class="amenities-icon">
            <img src="@/assets/image/surface2.png" alt="" v-if="roomDetail.amenities['Mini-Bar'] === true" class="icon">
            <img src="@/assets/image/surface2.png" alt="" v-else style="opacity: 0.2;" class="icon">
            <img src="@/assets/image/correct.png" alt="" class="mark" v-if="roomDetail.amenities['Mini-Bar'] === true">
            <img src="@/assets/image/false.png" alt="" class="mark" v-else style="opacity: 0.2;">
          </div>
          <div class="amenities-icon">
            <img src="@/assets/image/surface3.png" alt="" v-if="roomDetail.amenities['Room-Service'] === true" class="icon">
            <img src="@/assets/image/surface3.png" alt="" v-else style="opacity: 0.2;" class="icon">
            <img src="@/assets/image/correct.png" alt="" class="mark" v-if="roomDetail.amenities['Room-Service'] === true">
            <img src="@/assets/image/false.png" alt="" class="mark" v-else style="opacity: 0.2;">
          </div>
          <div class="amenities-icon">
            <img src="@/assets/image/surface4.png" alt="" v-if="roomDetail.amenities['Wi-Fi'] === true" class="icon">
            <img src="@/assets/image/surface4.png" alt="" v-else style="opacity: 0.2;" class="icon">
            <img src="@/assets/image/correct.png" alt="" class="mark" v-if="roomDetail.amenities['Wi-Fi'] === true">
            <img src="@/assets/image/false.png" alt="" class="mark" v-else style="opacity: 0.2;">
          </div>
          <div class="amenities-icon">
            <img src="@/assets/image/surface5.png" alt="" v-if="roomDetail.amenities['Child-Friendly'] === true" class="icon">
            <img src="@/assets/image/surface5.png" alt="" v-else style="opacity: 0.2;" class="icon">
            <img src="@/assets/image/correct.png" alt="" class="mark" v-if="roomDetail.amenities['Child-Friendly']=== true">
            <img src="@/assets/image/false.png" alt="" class="mark" v-else style="opacity: 0.2;">
          </div>
          <div class="amenities-icon">
            <img src="@/assets/image/surface6.png" alt="" v-if="roomDetail.amenities.Television === true" class="icon">
            <img src="@/assets/image/surface6.png" alt="" v-else style="opacity: 0.2;" class="icon">
            <img src="@/assets/image/correct.png" alt="" class="mark" v-if="roomDetail.amenities.Television=== true">
            <img src="@/assets/image/false.png" alt="" class="mark" v-else style="opacity: 0.2;">
          </div>
          <div class="amenities-icon">
            <img src="@/assets/image/surface7.png" alt="" v-if="roomDetail.amenities['Great-View'] === true" class="icon">
            <img src="@/assets/image/surface7.png" alt="" v-else style="opacity: 0.2;" class="icon">
            <img src="@/assets/image/correct.png" alt="" class="mark" v-if="roomDetail.amenities['Great-View'] === true">
            <img src="@/assets/image/false.png" alt="" class="mark" v-else style="opacity: 0.2;">
          </div>
          <div class="amenities-icon">
            <img src="@/assets/image/surface8.png" alt="" v-if="roomDetail.amenities.Refrigerator === true" class="icon">
            <img src="@/assets/image/surface8.png" alt="" v-else style="opacity: 0.2;" class="icon">
            <img src="@/assets/image/correct.png" alt="" class="mark" v-if="roomDetail.amenities.Refrigerator === true">
            <img src="@/assets/image/false.png" alt="" class="mark" v-else style="opacity: 0.2;">
          </div>
          <div class="amenities-icon">
            <img src="@/assets/image/surface9.png" alt="" v-if="roomDetail.amenities.Sofa === true" class="icon">
            <img src="@/assets/image/surface9.png" alt="" v-else style="opacity: 0.2;" class="icon">
            <img src="@/assets/image/correct.png" alt="" class="mark" v-if="roomDetail.amenities.Sofa  === true">
            <img src="@/assets/image/false.png" alt="" class="mark" v-else style="opacity: 0.2;">
          </div>
          <div class="amenities-icon">
            <img src="@/assets/image/surface10.png" alt="" v-if="roomDetail.amenities['Pet-Friendly'] === true" class="icon">
            <img src="@/assets/image/surface10.png" alt="" v-else style="opacity: 0.2;" class="icon">
            <img src="@/assets/image/correct.png" alt="" class="mark" v-if="roomDetail.amenities['Pet-Friendly']  === true">
            <img src="@/assets/image/false.png" alt="" class="mark" v-else style="opacity: 0.2;">
          </div>
          <div class="amenities-icon">
            <img src="@/assets/image/surface11.png" alt="" v-if="roomDetail.amenities['Smoke-Free'] === true" class="icon">
            <img src="@/assets/image/surface11.png" alt="" v-else style="opacity: 0.2;" class="icon">
            <img src="@/assets/image/correct.png" alt="" class="mark" v-if="roomDetail.amenities['Smoke-Free']  === true">
            <img src="@/assets/image/false.png" alt="" class="mark" v-else style="opacity: 0.2;">
          </div>
          <div class="amenities-icon">
            <img src="@/assets/image/surface12.png" alt="" v-if="roomDetail.amenities['Air-Conditioner'] === true" class="icon">
            <img src="@/assets/image/surface12.png" alt="" v-else style="opacity: 0.2;" class="icon">
            <img src="@/assets/image/correct.png" alt="" class="mark" v-if="roomDetail.amenities['Air-Conditioner']  === true">
            <img src="@/assets/image/false.png" alt="" class="mark" v-else style="opacity: 0.2;">
          </div>
        </div>
        <!-- Calender -->
        <calendar
        :allBookingData = "allBookingData"
        ></calendar>
      </div>
      <!-- Modal -->
      <div class="modal" v-if="modalShow">
        <div id="finish-modal" class="modal-overlay">
          <div class="modal-outSide">
            <div class="modal-content">
              <div class="close" @click="modalShow = false"><i class="fas fa-times"></i></div>
              <div class="modal-body">
                <ValidationObserver class="modal-form" v-slot="{ handleSubmit }">
                  <form @submit.prevent="handleSubmit(addBooking)">
                    <div class="name">
                        <label for="name">姓名</label>
                        <ValidationProvider rules="required" v-slot="{ errors }" name="name">
                          <input type="text" name="name" id="name" v-model="form.name"
                          :class="{ 'is-invalid': errors[0] }" placeholder="請輸入姓名">
                          <div class="font fontC-danger">{{ errors[0] }}</div>
                        </ValidationProvider>
                    </div>
                    <div class="phone">
                        <label for="phone">手機號碼</label>
                        <ValidationProvider rules="required|numeric|min:8|max:10" v-slot="{ errors }" name="phone">
                          <input type="tel" name="phone" id="phone" v-model="form.tel"
                          :class="{ 'is-invalid': errors[0] }" placeholder="09XX-XXX-XXX">
                          <div class="font fontC-danger">{{ errors[0] }}</div>
                        </ValidationProvider>
                    </div>
                    <div class="checkIn">
                        <label for="checkIn">入住日期</label>
                        <input type="text" name="checkIn" id="checkIn" v-model="checkInDay"
                        :placeholder="checkInPlaceholder" onfocus="(this.type='date')"
                        min="2020/10/4">
                    </div>
                    <div class="checkOut">
                        <label for="checkOut">退房日期</label>
                        <input type="text" name="checkOut" id="checkOut" v-model="checkOutDay"
                        :placeholder="checkOutPlaceholder" onfocus="(this.type='date')">
                    </div>
                    <p class="font font-h7 fontC-secondary">{{dayCounting}}天，{{normalOrHoliday}}</p>
                    <hr>
                    <p class="font font-h7 fontC-light">總計</p>
                    <p class="font font-display3 fontC-light">{{totalPrice|currency}}</p>
                    <button class="btn-lg btn-lg-primary" type="submit">確認送出</button>
                    <p class="font font-h8 fontC-light noPay">此預約系統僅預約功能，並不會對您進行收費</p>
                  </form>
                </ValidationObserver>
                <div class="modal-detail">
                  <!-- <div class="close" @click.prevent="modalShow = false"><i class="fas fa-times"></i></div> -->
                  <p class="font font-h2 fontC-primary">{{roomDetail.name}}</p>
                  <p class="font font-h7 fontC-primary">
                    <span>{{filterGuest}}人．</span>
                    <span>{{bedKind}}床．</span>
                    <span v-if="roomDetail.amenities.Breakfast === true">附早餐．</span>
                    <span>衛浴{{roomDetail.descriptionShort['Private-Bath']}}間．</span>
                    <span>{{roomDetail.descriptionShort.Footage}}平方公尺</span>
                  </p>
                  <p class="font font-h7 fontC-primary">
                    <span>平日（一~四）價格：{{roomDetail.normalDayPrice|currency}}／</span>
                    <span>假日（五~日）價格：{{roomDetail.holidayPrice|currency}}</span>
                  </p>
                  <div class="amenities">
                    <div class="amenities-icon" v-if="roomDetail.amenities.Breakfast === true">
                      <img src="@/assets/image/surface1.png" alt="" class="icon-S">
                    </div>
                    <div class="amenities-icon" v-if="roomDetail.amenities['Mini-Bar'] === true">
                      <img src="@/assets/image/surface2.png" alt="" class="icon-S">
                    </div>
                    <div class="amenities-icon" v-if="roomDetail.amenities['Room-Service'] === true">
                      <img src="@/assets/image/surface3.png" alt="" class="icon-S">
                    </div>
                    <div class="amenities-icon" v-if="roomDetail.amenities['Wi-Fi'] === true">
                      <img src="@/assets/image/surface4.png" alt="" class="icon-S">
                    </div>
                    <div class="amenities-icon" v-if="roomDetail.amenities['Child-Friendly'] === true">
                      <img src="@/assets/image/surface5.png" alt="" class="icon-S">
                    </div>
                    <div class="amenities-icon" v-if="roomDetail.amenities.Television === true">
                      <img src="@/assets/image/surface6.png" alt="" class="icon-S">
                    </div>
                    <div class="amenities-icon" v-if="roomDetail.amenities['Great-View'] === true">
                      <img src="@/assets/image/surface7.png" alt="" class="icon-S">
                    </div>
                    <div class="amenities-icon" v-if="roomDetail.amenities.Refrigerator === true">
                      <img src="@/assets/image/surface8.png" alt="" class="icon-S">
                    </div>
                    <div class="amenities-icon" v-if="roomDetail.amenities.Sofa === true">
                      <img src="@/assets/image/surface9.png" alt="" class="icon-S">
                    </div>
                    <div class="amenities-icon" v-if="roomDetail.amenities['Pet-Friendly'] === true">
                      <img src="@/assets/image/surface10.png" alt="" class="icon-S">
                    </div>
                    <div class="amenities-icon" v-if="roomDetail.amenities['Smoke-Free'] === true">
                      <img src="@/assets/image/surface11.png" alt="" class="icon-S">
                    </div>
                    <div class="amenities-icon" v-if="roomDetail.amenities['Air-Conditioner'] === true">
                      <img src="@/assets/image/surface12.png" alt="" class="icon-S">
                    </div>
                  </div>
                  <div class="rules">
                    <p class="font font-h6 fontC-primary">訂房資訊</p>
                    <p class="font font-h7 fontC-primary">．入住時間：最早15：00，最晚21：00；退房時間：10：00，請自行確認時間安排。</p>
                    <p class="font font-h7 fontC-primary">．平日定義為周一至周四，假日定義週五至週日及國定假日。</p>
                    <p class="font font-h7 fontC-primary">．若您有任何問題，歡迎撥打 03-8321155（服務時間 周一至周六 10：00－18：00）</p>
                  </div>
                  <div class="process">
                    <p class="font font-h6 fontC-primary">預約流程</p>
                    <div class="process-inside">
                      <div class="process-pic">
                        <div class="process-detail">
                          <img src="@/assets/image/process1.svg" alt="" class="process-icon">
                        </div>
                        <div class="process-text">
                          <p class="font font-h8 fontC-primary">
                            送出線上預約單
                          </p>
                        </div>
                      </div>
                      <img src="@/assets/image/arrow.svg" alt="" class="arrow">
                      <div class="process-pic">
                        <div class="process-detail">
                          <img src="@/assets/image/process2.svg" alt="" class="process-icon">
                        </div>
                        <div class="process-text">
                          <p class="font font-h8 fontC-primary">
                            系統立即回覆是否預約成功<br>並以簡訊發送訂房通知<br>(若未收到簡訊請來電確認)
                          </p>
                        </div>
                      </div>
                      <img src="@/assets/image/arrow.svg" alt="" class="arrow">
                      <div class="process-pic">
                        <div class="process-detail">
                          <img src="@/assets/image/process3.svg" alt="" class="process-icon">
                        </div>
                        <div class="process-text">
                          <p class="font font-h8 fontC-primary">
                            入住當日憑訂房通知<br>以現金或刷卡付款即可<br>(僅接受VISA.JSB.銀聯卡)
                          </p>
                        </div>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      <success
        v-if="isSuccess"
        @close = "onModalSuccessClose"
      ></success>
      <default
        v-if="isDefault"
        @close = "onModalDefaultClose"
      ></default>
    </template>
  </div>
</template>
<script>
import Success from '@/components/Success'
import Default from '@/components/Default'
import Calendar from '@/components/Calendar'

export default {
  components: {
    Success,
    Default,
    Calendar
  },
  data () {
    return {
      roomId: '',
      roomDetail: {},
      imageUrl: [],
      isloaded: false,
      modalShow: false,
      isSuccess: false,
      isDefault: false,
      form: {
        name: '',
        tel: '',
        date: []
      },
      checkInDay: '',
      checkOutDay: '',
      dayCount: '',
      bedKind: '',
      allBookingData: []
    }
  },
  methods: {
    gotoRoom () {
      const roomId = this.$route.params.id
      return this.axios({
        method: 'get',
        baseURL: `https://challenge.thef2e.com/api/thef2e2019/stage6/room/${roomId}`,
        headers: {
          Authorization: 'Bearer ZpNjg6fR488qhR6rBqkJUPUxciEgE5JfKKuvTBSEa8WyQu5ifFDykP9yVJQt',
          'Content-Type': 'application/json'
        }
      })
        .then((response) => {
          // console.log(response.data.room[0])
          // vm.roomName = response.data.room.name
          this.allBookingData = response.data.booking
          this.roomDetail = response.data.room[0]
          this.imageUrl = this.roomDetail.imageUrl.filter((item, index) => { return index === 1 })
          // console.log(this.imageUrl)
          console.log(this.allBookingData)
        })
        .finally(() => {
          this.isloaded = true
        })
      // this.$router.push('/SingleRoom')
    },
    addBooking () {
      const roomId = this.$route.params.id
      // const booking = this.form
      // console.log([this.form.date])
      // console.log(typeof this.form.date)
      this.axios({
        method: 'post',
        url: `https://challenge.thef2e.com/api/thef2e2019/stage6/room/${roomId}`,
        data: {
          name: this.form.name,
          tel: this.form.tel,
          date: this.formDate
        },
        headers: {
          Authorization: 'Bearer ZpNjg6fR488qhR6rBqkJUPUxciEgE5JfKKuvTBSEa8WyQu5ifFDykP9yVJQt'
        }
      })
        .then((response) => {
          // console.log(response.data)
          if (response.data.success === true) {
            this.isSuccess = !this.isSuccess
            // this.form.name = ''
            // this.form.tel = ''
            // this.checkInDay = ''
            // this.checkOutDay = ''
          } else {
            throw new Error('status Error')
          }
          // console.log(response.data.room)
        })
        .catch(e => {
          this.isDefault = !this.isDefault
          console.error(e)
          // eslint-disable-next-line no-proto
          console.log(e.__proto__)
        })
    },
    async calculateDate () {
      let day = ''
      const checkOutNew = new Date(this.checkOutDay)
      for (let i = 0; i < this.dayCounting; i++) {
        day = new Date(checkOutNew.valueOf() - (86400000 * (4 - i)))
        // console.log(day)
        // const newDay = `${day.getFullYear()}-${this.fixNumber(day.getMonth() + 1)}-${day.getDate()}`
        const newDay = `${day.getFullYear()}-${this.fixNumber(day.getMonth() + 1)}-${this.fixNumber(day.getDate())}`
        this.form.date.push(newDay)
      }
      // console.log(this.form.date)
      await this.addBooking()
    },
    fixNumber (num) {
      const strNum = String(num)
      if (strNum.length < 2) {
        return `0${strNum}`
      }
      return strNum
    },
    onModalSuccessClose () {
      this.isSuccess = false
      this.modalShow = false
    },
    onModalDefaultClose () {
      this.isDefault = false
      this.modalShow = false
    },
    filterBed () {
      if (this.roomDetail && this.roomDetail.descriptionShort) {/**/}
      switch (this.roomDetail.descriptionShort.Bed[0]) {
        case 'Single':
          this.bedKind = '單人'
          break
        case 'Double':
          this.bedKind = '雙人'
          break
        case 'Small Double':
          this.bedKind = '小雙人'
          break
        case 'Queen':
          this.bedKind = '大雙人'
      }
    }
  },
  computed: {
    dayCounting () {
      return (new Date(this.checkOutDay).valueOf() - new Date(this.checkInDay).valueOf()) / 86400000
    },
    formDate () {
      let day = ''
      const form = []
      const checkOutNew = new Date(this.checkOutDay)
      for (let i = 0; i < this.dayCounting; i++) {
        day = new Date(checkOutNew.valueOf() - (86400000 * (this.dayCounting - i)))
        const newDay = `${day.getFullYear()}-${this.fixNumber(day.getMonth() + 1)}-${this.fixNumber(day.getDate())}`
        // console.log(newDay)
        form.push(newDay)
      }
      return form
    },
    normalOrHoliday () {
      let week = 0
      const normal = []
      const holiday = []
      this.formDate.forEach(day => {
        week = (new Date(day)).getDay()
        if (week < 5) {
          normal.push(week)
        } else { holiday.push(week) }
      })
      return `${normal.length}晚平日${holiday.length}晚假日`
    },
    totalPrice () {
      let week = 0
      const normal = []
      const holiday = []
      this.formDate.forEach(day => {
        week = (new Date(day)).getDay()
        if (week < 5) {
          normal.push(week)
        } else { holiday.push(week) }
      })
      return normal.length * this.roomDetail.normalDayPrice + holiday.length * this.roomDetail.holidayPrice
    },
    today () {
      const day = new Date().getDay()
      return day < 5 ? this.roomDetail.normalDayPrice : this.roomDetail.holidayPrice
    },
    filterGuest () {
      return this.roomDetail.descriptionShort.GuestMin === this.roomDetail.descriptionShort.GuestMax ? this.roomDetail.descriptionShort.GuestMin : `${this.roomDetail.descriptionShort.GuestMin}-${this.roomDetail.descriptionShort.GuestMax}`
    },
    checkInPlaceholder () {
      return `${new Date().getFullYear()}/${new Date().getMonth() + 1}/${new Date().getDate()}`
    },
    checkOutPlaceholder () {
      const d = new Date().valueOf() + 86400000
      return `${new Date(d).getFullYear()}/${new Date(d).getMonth() + 1}/${new Date(d).getDate()}`
    }
  },
  async created () {
    await this.gotoRoom()
    // this.calculateDate()
    this.filterBed()
  }
}
</script>
<style lang="scss">
.photo-layer {
  background: transparent linear-gradient(to bottom, #FFFFFF00 0%, #FFFFFF 100%) 0% 0% no-repeat padding-box;
}
</style>
