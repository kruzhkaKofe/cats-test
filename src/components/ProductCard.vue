<template>
  <div
    class="card"
    @mouseleave="isMouseLeave"
    v-for="(card, id) in cards"
    :key="id"
    :class="{
      active: isActive(card),
      disabled: card.available === false,
      unhover: isActive(card) && approve === false,
    }"
  >
    <div class="card__cover" @click="chooseCard(card)">
      <div class="card__corner"></div>

      <span
        v-if="isActive(card) && approve === false"
        class="card__description"
      >
        Котэ не одобряет?
      </span>
      <span v-else class="card__description">Cказачное заморское яство</span>

      <h2 class="card__title">Нямушка</h2>
      <span class="card__sort">{{ card.sort }}</span>
      <ul class="card__list">
        <li class="card__list-item" v-for="(vol, i) in card.volume" :key="i">
          {{ vol }}
        </li>
      </ul>
      <img class="card__image" src="@/assets/cat.png" alt="cat" />
      <div class="card__circle">
        <div class="card__weight">
          <div class="card__weight-num">
            {{ card.weight }}
          </div>
          <div class="card__weight-messure">кг</div>
        </div>
      </div>
    </div>

    <div v-if="isActive(card) && card.available" class="card__footer">
      {{ card.sklad }}
    </div>

    <div v-else-if="card.available === false" class="card__footer">
      Печалька, {{ card.sort }} закончился.
    </div>

    <div class="card__footer" v-else>
      Чего сидишь? Порадуй котэ,
      <button @click="chooseCard(card)" class="card__footer-button">
        купи.
      </button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    cards: {
      type: Array,
      required: true,
    },
  },

  data() {
    return {
      cart: [],
      approve: true,
    };
  },

  methods: {
    chooseCard(card) {
      if (card.available === false) {
        return;
      }
      if (this.cart.find((i) => i === card)) {
        this.cart = this.cart.filter((el) => el != card);
      } else {
        this.cart.push(card);
        this.approve = true;
      }
    },

    isActive(card) {
      if (this.cart.find((i) => i === card)) {
        return true;
      }
    },

    isMouseLeave(e) {
      if (this.isActive && e !== ".card") {
        this.approve = false;
      } else {
        return;
      }
    },
  },
};
</script>

<style lang="sass" scoped>

.active .card__cover
	border: 4px solid $pink

.active .card__circle
	background-color: $pink

.active .card__corner
	border-top: 42px solid $pink

.unhover .card__description
	color: $pink

.disabled	.card__cover
	cursor: default
	border: 4px solid $gray

.disabled .card__corner
	border-top: 42px solid $gray

.disabled .card__circle
	background-color: $gray

.disabled .card__footer
	color: $yellow

.disabled	.card__description,
.disabled	.card__title,
.disabled	.card__sort,
.disabled	.card__list,
.disabled .card__image
	color: $gray
	opacity: 0.5


.card
	width: 320px
	height: 510px
	margin: 25px 40px

	@media (max-width: $bp-medium)
		margin: 25px 20px

	&__cover
		position: relative
		width: 100%
		height: 480px
		padding: 20px 50px
		background-color: $dirt-white
		border-radius: 12px
		cursor: pointer
		overflow: hidden
		border: 4px solid $blue
		border-radius: 12px
		clip-path: polygon(44px 0, 100% 0, 100% 0, 100% 100%, 0 100%, 0 44px)

	&__corner
		position: absolute
		top: 0
		left: 0
		width: 0
		height: 0
		border-top: 42px solid $blue 
		border-right: 42px solid transparent

	&__description
		display: inline-block
		font-size: 16px
		line-height: 19px
		color: $dark-gray
		margin-bottom: 5px

	&__title
		font-weight: 700
		font-size: 48px
		line-height: 56px
		color: $black

	&__sort
		display: inline-block
		font-weight: 700
		font-size: 24px
		line-height: 28px
		color: $black
		margin-bottom: 15px

	&__list
		position: absolute
		font-weight: 700
		font-size: 14px
		line-height: 16px
		color: $dark-gray
		z-index: 2

	&__image
		position: absolute
		top: 208px
		left: 0
		z-index: 0

	&__circle
		position: absolute
		z-index: 10
		display: flex
		justify-content: center
		align-items: center
		text-align: center
		width: 80px
		height: 80px
		border-radius: 50%
		background-color: $blue
		color: $white
		font-size: 42px
		line-height: 22px
		bottom: 16px
		right: 16px

	&__weight

		&-num
			display: flex
			align-items: center
			height: 36px

		&-messure
			font-size: 21px

	&__footer
		margin-top: 15px
		color: $white
		font-size: 13px
		line-height: 15px
		text-align: center

		&-button
			color: $blue
			font-weight: 700
			background-color: transparent
			cursor: pointer
			text-decoration: dotted underline
			border: transparent
</style>
