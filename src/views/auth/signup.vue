<template>
  <div id="body" style="padding-top: 5%">
    <div>
      <b-row id="b-row" align-h="center">
        <b-col id="b-col" cols="3">
          <b-card id="b-card" title="회원가입">
            <b-form-group>
              <label for="userId">아이디</label>
              <b-form-input
                id="userId"
                ref="userId"
                v-model="user.userId"
                :state="userIdState"
                aria-describedby="아이디"
                required
                size="sm"
                trim
              ></b-form-input>

              <!-- 조건 미충족 시 -->
              <b-form-invalid-feedback v-if="user.userId" id="input-live-feedback">
                아이디는 영문 대소문자와 <br />
                숫자 5-12자리로 입력해야 합니다
              </b-form-invalid-feedback>

              <!-- 조건 충족 시 -->
              <b-form-text v-if="user.userId" id="input-live-help"></b-form-text>
            </b-form-group>

            <b-form-group>
              <label for="userPw">비밀번호</label>
              <b-form-input
                id="userPw"
                ref="userPw"
                v-model="user.userPw"
                :state="userPwState"
                aria-describedby="비밀번호"
                type="password"
                size="sm"
                required
                trim
              ></b-form-input>

              <!-- 조건 미충족 시 -->
              <b-form-invalid-feedback v-if="user.userPw" id="input-live-feedback">
                비밀번호는 영문 대소문자, 숫자,<br />
                특수문자 8-20자리로 입력해야 합니다
              </b-form-invalid-feedback>

              <!-- 조건 충족 시 -->
              <b-form-text v-if="user.userPw" id="input-live-help"></b-form-text>
            </b-form-group>

            <b-form-group>
              <label for="userPw">비밀번호 재확인</label>
              <b-form-input
                id="userPwCheck"
                ref="userPwCheck"
                v-model="user.userPwCheck"
                :state="userPwCheckState"
                aria-describedby="비밀번호 재확인"
                type="password"
                size="sm"
                required
                trim
              ></b-form-input>

              <!-- 조건 미충족 시 -->
              <b-form-invalid-feedback v-if="user.userPwCheck" id="input-live-feedback">
                비밀번호가 일치하지 않습니다.
              </b-form-invalid-feedback>

              <!-- 조건 충족 시 -->
              <b-form-text v-if="user.userPwCheck" id="input-live-help"></b-form-text>
            </b-form-group>

            <b-form-group>
              <label for="userName">이름</label>
              <b-form-input
                id="userName"
                ref="userName"
                v-model="user.userName"
                :state="userNameState"
                aria-describedby="이름"
                size="sm"
                required
                trim
              ></b-form-input>

              <!-- 조건 미충족 시 -->
              <b-form-invalid-feedback v-if="user.userName" id="input-live-feedback">
                이름은 한글 2자리 이상 입력해야 합니다
              </b-form-invalid-feedback>

              <!-- 조건 충족 시 -->
              <b-form-text v-if="user.userName" id="input-live-help"></b-form-text>
            </b-form-group>

            <b-form-group>
              <label for="userEmail">이메일</label>
              <b-form-input
                id="userEmail"
                ref="userEmail"
                v-model="user.userEmail"
                aria-describedby="이메일"
                type="email"
                placeholder="example@example.com"
                size="sm"
                required
                :state="userEmailState"
                trim
              ></b-form-input>

              <!-- 조건 미충족 시 -->
              <b-form-invalid-feedback v-if="user.userEmail" id="input-live-feedback">
                이메일 형식이 다릅니다
              </b-form-invalid-feedback>

              <!-- 조건 충족 시 -->
              <b-form-text v-if="user.userEmail" id="input-live-help"></b-form-text>
            </b-form-group>

            <b-form-group>
              <label for="userPhoneNumber">핸드폰 번호</label>
              <b-form-input
                id="userPhoneNumber"
                ref="userPhoneNumber"
                v-model="user.userPhoneNumber"
                aria-describedby="핸드폰 번호"
                placeholder="000-0000-0000"
                type="text"
                size="sm"
                :formatter="formatNumber"
                required
                trim
                @keyup="getPhoneMask(user.userPhoneNumber)"
              ></b-form-input>
            </b-form-group>

            <b-form-group>
              <label for="userEmail">생년월일</label>
              <b-form-input
                id="userBirth"
                ref="userBirth"
                v-model="user.userBirth"
                aria-describedby="생년월일"
                type="date"
                size="sm"
                required
                trim
              ></b-form-input>
            </b-form-group>

            <b-form-group class="daummap">
              <b-row align-h="center">
                <label for="userAddress">주소</label>
                <b-col cols="5">
                  <b-form-input
                    id="userZip"
                    v-model="user.userZip"
                    type="text"
                    placeholder="우편번호"
                    size="sm"
                  ></b-form-input>
                </b-col>
                <b-col> <b-button id="showApi" size="sm" @click="showApi">우편번호 찾기</b-button></b-col>
                <b-form-input
                  id="userAddr1"
                  v-model="user.userAddr1"
                  type="text"
                  placeholder="주소"
                  size="sm"
                ></b-form-input>
                <b-form-input
                  id="userAddr2"
                  v-model="user.userAddr2"
                  type="text"
                  placeholder="상세주소"
                  size="sm"
                ></b-form-input>
              </b-row>
            </b-form-group>
          </b-card>
          <button class="btn btn-primary" @click="onSubmit">회원가입</button>
        </b-col>
      </b-row>
    </div>
  </div>
</template>

<script>
export default {
  // name: 'Daummap',
  data() {
    return {
      user: {
        userId: '',
        userPw: '',
        userPwCheck: '',
        userName: '',
        userEmail: '',
        userPhoneNumber: '',
        userBirth: '',
        userZip: '',
        userAddr1: '',
        userAddr2: ''
      }
    }
  },
  computed: {
    userIdState() {
      return this.user.userId.length > 4 && this.user.userId.length < 13 && /^[a-zA-Z0-9]*$/.test(this.user.userId)
    },
    userPwState() {
      return (
        this.user.userPw.length > 7 &&
        this.user.userPw.length < 21 &&
        /^(?=.*[a-zA-Z])(?=.*[0-9])(?=.*[!@#$%^&*])[a-zA-Z0-9!@#$%^&*]*$/.test(this.user.userPw)
      ) // 영문 대문자+소문자+특수문자 8-20자리
    },
    userPwCheckState() {
      return this.user.userPwCheck === this.user.userPw
    },
    userNameState() {
      return this.user.userName.length > 1 && /^[가-힣]*$/.test(this.user.userName) // 한글 2자리 이상
    },
    userEmailState() {
      return (
        this.user.userEmail.length > 5 &&
        /^[A-Za-z0-9_]+[A-Za-z0-9]*[@]{1}[A-Za-z0-9]+[A-Za-z0-9]*[.]{1}[A-Za-z]{1,3}$/.test(this.user.userEmail)
      ) // 이메일 형식(영문대소문자/숫자+@+영문대소문자/숫자+.+영문대소문자 3자리)
    },
    signResult() {
      return this.$store.getters.UserInsertedResult
    }
  },
  watch: {
    signResult(value) {
      // console.log('watch.signResult', value)

      // 회원가입에 성공한 경우
      if (value === true) {
        alert('회원가입 되었습니다')
        this.$router.replace('/auth/login') // 히스토리 기록 안남음
      } else if (value === false) {
        alert('이미 존재하는 회원입니다')
      }
    }
  },
  methods: {
    // 공란 및 유효성 여부 체크
    checkInput() {
      const inputForm = this.user
      // console.log(inputForm)
      if (inputForm.userId == '') {
        alert('아이디를 입력해 주세요')
        this.$refs.userId.focus()
        return false
      } else if (this.userIdState === false) {
        this.$refs.userId.focus()
        return false
      }

      if (inputForm.userPw == '') {
        alert('비밀번호를 입력해 주세요')
        this.$refs.userPw.focus()
        return false
      } else if (this.userPwState === false) {
        this.$refs.userPw.focus()
        return false
      }

      if (inputForm.userPwCheck == '') {
        alert('비밀번호를 확인해 주세요')
        this.$refs.userPwCheck.focus()
        return false
      } else if (this.userPwCheckState === false) {
        this.$refs.userPwCheck.focus()
        return false
      }

      if (inputForm.userName == '') {
        alert('이름을 입력해 주세요')
        this.$refs.userName.focus()
        return false
      } else if (this.userNameState === false) {
        this.$refs.userName.focus()
        return false
      }

      if (inputForm.userEmail == '') {
        alert('이메일을 입력해 주세요')
        this.$refs.userEmail.focus()
        return false
      } else if (this.userEmailState === false) {
        this.$refs.userEmail.focus()
        return false
      }

      if (inputForm.userPhoneNumber == '') {
        alert('전화번호를 입력해 주세요')
        this.$refs.userPhoneNumber.focus()
        return false
      } else if (this.formatNumber === false) {
        alert('전화번호를 확인해 주세요')
        this.$refs.userPhoneNumber.focus()
        return false
      }

      if (inputForm.userBirth == '') {
        alert('생년월일을 입력해 주세요')
        this.$refs.userBirth.focus()
        return false
      } else {
        return true
      }
    },

    // 전화번호 글자수 제한
    formatNumber(e) {
      return String(e).substring(0, 13) // 최대 11자리 010-1234-5678
    },

    // 전화번호 숫자만 입력 시 파이프(-) 자동 입력
    getPhoneMask(val) {
      let res = this.getMask(val)
      this.user.userPhoneNumber = res

      // // 서버 전송 값에는 '-'를 제외하고 숫자만 저장
      // this.$store.getters.User.userPhoneNumber = this.user.userPhoneNumber.replace(/[^0-9]/g, '')
    },

    getMask(inputNumber) {
      if (!inputNumber) return inputNumber
      inputNumber = inputNumber.replace(/[^0-9]/g, '')

      let res = ''
      if (inputNumber.length < 8) {
        res = inputNumber
      } else if (inputNumber.length == 8) {
        res = inputNumber.substr(0, 4) + '-' + inputNumber.substr(4)
      } else if (inputNumber.length == 9) {
        res = inputNumber.substr(0, 3) + '-' + inputNumber.substr(3, 3) + '-' + inputNumber.substr(6)
      } else if (inputNumber.length == 10) {
        res = inputNumber.substr(0, 3) + '-' + inputNumber.substr(3, 3) + '-' + inputNumber.substr(6)
      } else if (inputNumber.length > 10) {
        res = inputNumber.substr(0, 3) + '-' + inputNumber.substr(3, 4) + '-' + inputNumber.substr(7)
      }
      //   }
      // }
      return res
    },

    // 우편번호 찾기 다음 우편번호 서비스 api 연동
    showApi() {
      new window.daum.Postcode({
        oncomplete: data => {
          // 팝업에서 검색결과 항목을 클릭했을 때 실행할 코드를 작성하는 부분

          // 도로명 주소의 노출 규칙에 따라 주소를 조합한다.
          // 내려오는 변수가 값이 없는 경우엔 공백('') 값을 가지므로, 이를 참고하여 분기 한다.
          let fullRoadAddr = data.roadAddress // 도로명 주소 변수
          let extraRoadAddr = '' // 도로명 조합형 주소 변수

          // 법정동명이 있을 경우 추가한다. (법정리는 제외)
          // 법정동의 경우 마지막 문자가 "동/로/가"로 끝난다.
          if (data.bname !== '' && /[동|로|가]$/g.test(data.bname)) {
            extraRoadAddr += data.bname
          }
          // 건물명이 있고, 공동주택일 경우 추가한다.
          if (data.buildingName !== '' && data.apartment === 'Y') {
            extraRoadAddr += extraRoadAddr !== '' ? ', ' + data.buildingName : data.buildingName
          }
          // 도로명, 지번 조합형 주소가 있을 경우, 괄호까지 추가한 최종 문자열을 만든다.
          if (extraRoadAddr !== '') {
            extraRoadAddr = ' (' + extraRoadAddr + ')'
          }
          // 도로명, 지번 주소의 유무에 따라 해당 조합형 주소를 추가한다.
          if (fullRoadAddr !== '') {
            fullRoadAddr += extraRoadAddr
          }

          // 우편번호와 주소 정보를 해당 필드에 넣는다.
          this.user.userZip = data.zonecode // 5자리 새 우편번호 사용
          this.user.userAddr1 = fullRoadAddr
        }
      }).open()
    },
    // Sign 버튼 눌렀을 시
    onSubmit() {
      // console.log('onSubmit', { ...this.user })
      if (this.checkInput() === false) {
        return false
      } else {
        // 초기화
        this.$store.dispatch('actUserInit') // null값으로 초기화
        // 등록
        this.$store.dispatch('actUserInsert', this.user)
      }
    }
  }
}
</script>

<style lang="scss">
#body,
#b-row {
  width: 90vw;
  margin: auto;
  overflow-x: hidden;
}
#b-col {
  width: 30%;
  min-width: 460px;
  margin: auto;
}
#b-card {
  font-size: 1.4rem;
  width: 100%;
  padding-bottom: 20px;
  margin: auto;
  label {
    font-size: 0.8em;
    margin: 20px 0 10px;
  }
  input {
    border-radius: 20px;
    margin: 10px 0;
    text-align: center;
    width: 70%;
    margin: auto;
  }
  #input-live-feedback {
    font-size: 0.6em;
    line-height: 1.4em;
  }
}
.btn {
  background: $main;
  border: 0px;
}
.btn:hover {
  background: $sub;
}
.btn-primary {
  width: 100%;
  height: 50px;
}
#userZip {
  float: right;
  position: relative;
  margin-bottom: -26px;
  right: -6px;
}
#showApi {
  border-radius: 20px;
  padding: 5px 20px;
}
@media all and(max-width:767px) {
  #b-col {
    width: 100%;
  }
  #b-card {
    margin-top: 30px;
    font-size: 1.4em;
    width: 100%;
  }
}
</style>
