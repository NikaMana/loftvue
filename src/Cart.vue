<template>
	<div class="cart">

		<h1>КОРЗИНА</h1>
		<div class="row table-head">
			<div class="col-chek">Выделено <b>{{chek}}</b></div>
			<div class="del-chek">
				<span @click="delCheck"><button><i class="icon-cancel"></i></button><u>Удалить отмеченные</u></span>
			</div>
		</div>

		<div class="table-body">
		<div class="row" v-for="(item) in inCart">
			<div class="chek">
				<input type="checkbox" name="chek" v-model="item.checkedProd">{{item.id}}
			</div>			
			<div class="prewiew">
				<img :src="item.img" alt="placeholder+image">
			</div>
			<div class="title">{{item.title}}</div>
			<div class="col-1 text-gray">{{item.price}} Р</div>
			<div class="col-05 text-gray">x</div>
			<div class="col-1 text-gray">
				<input class="text-gray" type="text" name="qt" :value="item.qt" @click="showWindow(item.price, item.qt, item.id)" readonly>
			</div>			
			<div class="col-05">=</div>
			<div class="col-1">{{item.price*item.qt}} Р</div>			
		</div>

		<div class="row">
			<div class="pop-up" v-show="isShow">
				<p>Изменить количество</p>
				<div>{{tempPr}} x 
					<button type="button" @click="delQT()">-</button>
					<input type="text" name="qt" v-model="tempQT" readonly>
					<button type="button" @click="addQT()">+</button> 
					{{tempPr*tempQT}} Р
				</div>
				<p><u @click="saveNewQt()">СОХРАНИТЬ</u>
					<span @click="isShow = !isShow"><u>ОТМЕНИТЬ</u></span>
				</p>
			</div>
		</div>
		</div>	

		<div class="row">
			<div class="calc text-gray">
				<p>Промежуточный итог в корзине: </p>
				<p>В том числе НДС: </p>
			</div>
			<div class="rez">
				<p>{{promo}} Р</p>
				<p>{{nds}} Р</p>
			</div>
		</div>

		<div class="row">
			<div class="calc total">ИТОГО:</div>				
			<div class="total rez">{{total}} Р</div>
		</div>

	</div>
</template>
<script>
import inCart from '../product.json';
export default {
	
	data(){
		return {			
			inCart,
			isShow: false,
			tempQT: 0,
			tempPr: 0,
			tempId: 0
		}
	},
	computed: {
		promo() {
		      var promo = 0; 
		      for(var i = 0; i < this.inCart.length; i++) {
		        promo += this.inCart[i].price * this.inCart[i].qt;
		      }		      
		      return promo;
		},
		nds() {		      
		      return this.promo * 0.18;
		},
		total() {		      
		      return this.promo + this.nds;
		},
		chek(){
		    	var ckeck = 0;
		    	for(var i = 0; i < this.inCart.length; i++) {
			        if(this.inCart[i].checkedProd){
			        	ckeck++;
			        }
		      	}
		    	return ckeck;
		}
	},
	methods: {
		delCheck(){
				for(var i = 0; i < this.inCart.length; i++) {
					if(this.inCart[i].checkedProd){
						this.inCart.splice(i, this.chek);
					}
				}				
		},
		showWindow(price, qt, id){				
					this.isShow = !this.isShow;	
					this.tempPr = price;
					this.tempQT = qt;
					this.tempId	= id;			
		},
		delQT(){
				if(this.tempQT > 1){
					this.tempQT--;
				} else {
					alert("Товаров не может быть меньше 1!");
				}				
		},
		addQT(){
			if(this.tempQT > 1000){
				alert("Товаров не может быть больше 1000!");
			} else {
				this.tempQT++;
			}
		},		
		saveNewQt(){
		    	for(var i = 0; i < this.inCart.length; i++) {
					if(this.inCart[i].id === this.tempId){
						this.inCart[i].qt = this.tempQT;
						this.isShow = !this.isShow;	
					}				
				}			    
		}
	}
}	
</script>