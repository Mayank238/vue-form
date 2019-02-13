<template>
	<div>
		<form>
			<div v-if='seen'>
			  <div class="container box">
				  <p class="txt">Registration Form</p>
				  <div class="form-group">
				    <label class="form-control-label" >FirstName:</label>
				      <div>
				        <input type="text" name="" class="form-control col-lg-10"
				        :class='{err: focus.fname}' v-model="fname">
				      </div>
          </div>
          <div class="form-group">
				    <label class="form-control-label">LastName:</label>
				      <div>
				        <input type="text" name="" class="form-control col-lg-10"
				        :class="{err: focus.lname}" v-model="lname">
				      </div>
          </div>
          <div class="form-group">
				    <label class="form-control-label">E-mail:</label>
				      <div>
				        <input type="text" name="" class="form-control col-lg-10" v-model="email"
				        :class="{err: focus.email}">
				      </div>
          </div>
          <div class="form-group">
				    <label class="form-control-label">Phone-no:</label>
				      <div>
				        <input type="text" name="" class="form-control col-lg-10"
				        :class="{err: focus.phno}" v-model="phno">
				      </div>
          </div>
          <div class="form-group">
          	<button class="form-control col-lg-2 btn btn-primary" @click='Nextcomp'>Next</button>

          </div>
          <div class="fot">
          </div>
			  </div>
		  </div>
		  <div v-else>
			  <div class="container box">
				  <p class="txt">Account detail</p>
				  <div class="form-group">
				    <label class="form-control-label" >BankName:</label>
				      <div>
				        <input type="text" name="" class="form-control col-lg-10" v-model='Bname'
                :class = "{err: focus.Bname}">
				      </div>
          </div>
          <div class="form-group">
				    <label class="form-control-label">Branch:</label>
				      <div>
				        <input type="text" name="" class="form-control col-lg-10"
                :class="{err: focus.Bbranch}" v-model='Bbranch'>
				      </div>
          </div>
          <div class="form-group">
				    <label class="form-control-label">Account no:</label>
				      <div>
				        <input type="text" name="" class="form-control col-lg-10" v-model='Bacc'
                :class="{err: focus.Bacc}">
				      </div>
          </div>
          <div class="form-group">
				    <label class="form-control-label">IFSC code:</label>
				      <div>
				        <input type="text" name="" class="form-control col-lg-10" v-model='BIFSC'
                :class="{err: focus.BIFSC}">
				      </div>
          </div>
          <div class="form-group">
          	<button class="form-control col-lg-3 btn btn-primary" @click="Nextcomp">
          	Previous</button>
          	<button class="form-control col-lg-3 btn btn-primary" @click="store()">
          	Submit</button>
          </div>
          <div class="fot">

          </div>
			  </div>
		  </div>
		</form>
	</div>
</template>
<script>

	export default{
		data () {
            return {
                seen: true,
                fc: false,
                sc: false,
                fname:'',
                lname:'',
                phno:'',
                email:'',
                Bname:'',
                Bbranch:'',
                Bacc:'',
                BIFSC: '',
                focus: {
                	email: false,
                	fname: false,
                	lname: false,
                	phno: false,
                	Bname: false,
                	Bbranch: false,
                	Bacc : false,
                	BIFSC: false
                }

            }
        },
    methods:{
    Nextcomp(){
      this.seen = !this.seen;
      console.log(this.seen)
    },
    store(){
      this.fc = false
      this.sc = false
    	if (this.fname && this.lname && this.phno && this.email && this.validphone(this.phno) && this.validEmail(this.email)) {
    		this.fc = true


    	}
    	if(this.fc == false){

    		if (!this.fname) {
    			this.focus.fname = true
    		}
    		if (!this.lname) {
    			this.focus.lname = true
    		}
    		if (!this.phno || !this.validphone(this.phno)) {
    			this.focus.phno = true
    		}
    		if(!this.email || !this.validEmail(this.email) ){
    			this.focus.email = true
    		}
           this.seen=true
    	}
    	if (this.Bname && this.Bbranch && this.Bacc && this.BIFSC && this.valiacc(this.Bacc)) {
    		this.sc = true
        //this.focus.Bname = false
    	}

        if(!this.Bname.trim()){
          this.focus.Bname = true
        }else{
          this.focus.Bname = false
        }
        if (!this.Bbranch) {
          console.log("qwe")
          this.focus.Bbranch = true
        }else{
           this.focus.Bbranch = false
        }
        if (!this.Bacc || !this.valiacc(this.Bacc)) {
          this.focus.Bacc = true
        }else{
          this.focus.Bacc = false
        }
        if (!this.BIFSC) {
          this.focus.BIFSC = true
        }else{
          this.focus.BIFSC = false
        }

    	if (this.fc == true && this.sc == true) {
        this.focus.fname =false
        this.focus.lname =false
        this.focus.email =false
        this.focus.phno =false
        this.focus.Bbranch = false
        this.focus.Bname = false
        this.focus.Bacc = false
        this.focus.BIFSC = false
    		localStorage.setItem('firstname', this.fname )
    		localStorage.setItem('lastname',  this.lname )
    		localStorage.setItem('email',     this.email )
    		localStorage.setItem('Phone-no',  this.phno )
    		localStorage.setItem('BankName',  this.Bname )
    		localStorage.setItem('Bankbranch',this.Bbranch )
    		localStorage.setItem('Account no',this.Bacc )
    		localStorage.setItem('IFSC code', this.BIFSC )

    	}
    },
    validphone: function (phone) {
          var ph = /^[0-9]{1}[0-9]{9}$/;

          return ph.test(phone);
      },
    validEmail: function (email) {
         var re = /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
        return re.test(email);
      },
    valiacc: function (acc) {
          var ph = /^[0-9]{3}[0-9]{9}$/;

          return ph.test(acc);
      }
  }
	}
</script>
<style>
.box{
	margin-top: 10px;
	position: relative;
	width: 400px;
	background-color: rgb(204,228,234);
	color: black;
}
.txt{
	font-size: 20px;
	margin-left: 90px;
}
.fot{
	height: 30px;
	background-color: ;
}
.err{
	border: 1px solid red;
}

</style>
