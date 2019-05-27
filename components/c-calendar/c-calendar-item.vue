<template>
	<view>
		<block v-for="(weeks, week) in canlender.weeks" :key="week">
			<view class="c-calender__body-date-week">
				<block v-for="(day, index) in weeks" :key="index">
					<view :class="{
              'c-calender__disable': canlender.month !== day.month || day.disable,
              'c-calender__date-current':
                (day.date == canlender.date || day.checked) &&
                canlender.month == day.month &&
                !day.disable,
              'c-calender__lunar': lunar,
              'c-calender__active': day.isDay,
              'c-calender__is-day': day.isDay
            }" class="c-calender__date" @tap="
              selectDays(
                week,
                index,
                canlender.month === day.month,
                day.disable,
                canlender.lunar
              )
            ">
						<view class="c-calender__circle-box">
							{{ day.date }}
							<view v-if="lunar" class="c-calender__lunar">{{ day.lunar }}</view>
							<view v-if="day.have" class="c-calender__data-circle" />
						</view>
					</view>
				</block>
			</view>
		</block>
	</view>
</template>

<script>
	export default {
		name: 'UniCalendarItem',
		props: {
			/**
			 * 当前日期
			 */
			canlender: {
				type: null,
				default: () => {
					return {}
				}
			},
			lunar: {
				type: Boolean,
				default: false
			}
		},
		data() {
			return {}
		},
		created() {},
		methods: {
			selectDays(week, index, ischeck, isDay, lunar) {
				this.$emit('selectDays', {
					week,
					index,
					ischeck,
					isDay,
					lunar
				})
			}
		}
	}
</script>

<style>
	@charset "UTF-8";

	.c-calender__body-date-week {
		display: flex;
		width: 100%;
		border-bottom: 1px #f5f5f5 solid
	}

	.c-calender__body-date-week:last-child {
		border: none
	}

	.c-calender__body-date-week .c-calender__date {
		position: relative;
		width: 100%;
		text-align: center;
		display: flex;
		justify-content: center;
		align-items: center;
		color: #000;
		background: #fff;
		box-sizing: border-box;
		padding: 20upx 0;
		line-height: 1.5
	}

	.c-calender__body-date-week .c-calender__date .c-calender__lunar {
		font-size: 20upx;
		color: #000;
		line-height: 1.2
	}

	.c-calender__body-date-week .c-calender__date .c-calender__circle-box {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		width: 80upx;
		height: 80upx;
		flex-shrink: 0;
		border-radius: 50%;
		transition: all .2s;
		line-height: 1.2
	}

	.c-calender__body-date-week .c-calender__date.c-calender__disable {
		color: #d4d4d4
	}

	.c-calender__body-date-week .c-calender__date.c-calender__disable .c-calender__lunar {
		color: #d4d4d4
	}

	.c-calender__body-date-week .c-calender__date.c-calender__is-day {
		color: #fd2e32
	}

	.c-calender__body-date-week .c-calender__date.c-calender__is-day .c-calender__lunar {
		color: #fd2e32
	}

	.c-calender__body-date-week .c-calender__date.c-calender__date-current {
		color: #fff;
		box-sizing: border-box
	}

	.c-calender__body-date-week .c-calender__date.c-calender__date-current .c-calender__circle-box {
		background: #fd2e32
	}

	.c-calender__body-date-week .c-calender__date.c-calender__date-current .c-calender__lunar {
		color: #fff
	}

	.c-calender__body-date-week .c-calender__date .c-calender__data-circle {
		position: absolute;
		top: 10upx;
		right: 10upx;
		width: 10rpx;
		height: 10rpx;
		border-radius: 50%;
		background: #ff5a5f;
		z-index: 2
	}
</style>