<template>
    <div class="course-card-col" @click="routerGo">
        <div class="card-left">
            <div class="card-image">
                <div v-if="discount" class="course-tag">
                    <van-tag type="danger" size="medium" mark>限时</van-tag>
                </div>
                <img v-lazy="getImageUrl(image)" alt>
            </div>
        </div>
        <div class="card-right">
            <div class="card-title card-ellipsis">
                <span>{{title}}</span>
            </div>
            <div class="card-desc card-ellipsis">
                {{desc}}
            </div>
            <div class="card-bottom">
                <span class="info">{{sales}}人报名 {{rate?`| 好评${rate*100}%`:''}}</span>
                <span v-if="price > 0" class="price" style="color: #ee0a24;">{{price}} 课程币</span>
                <span v-else class="price" style="color: #42c02e;">免费</span>
            </div>
        </div>
    </div>
</template>

<script>
    import {getImageUrl} from "@/utils/url"
    import {Tag} from 'vant'

    export default {
        name: "CourseCardCol",
        props: {
            image: String,
            title: String,
            desc: String,
            discount: Boolean,
            sales: [Number, String],
            rate: [Number, String],
            price: [Number, String],
            id: [Number, String]
        },
        components: {'van-tag': Tag},
        data() {
            return {
                getImageUrl
            }
        },
        methods: {
            routerGo() {
                if (this.id) {
                    this.$router.push({name: 'course-study', params: {id: this.id.toString()}});
                }
            }
        }
    }
</script>

<style lang="less">
    .course-card-col {
        @card-width: 35.6vw;
        position: relative;
        padding: 10px 0 0;

        &:after {
            clear: both;
            content: "";
            display: table;
        }

        .card-left {
            position: relative;
            flex: none;
            width: @card-width;
            height: calc(@card-width * 9 / 16);
            float: left;

            .card-image {
                position: relative;
                display: inline-block;
                width: 100%;
                height: 100%;

                img {
                    width: 100%;
                    height: 100%;
                    object-fit: contain;
                    border-radius: 3px;
                }
            }

            .course-tag {
                position: absolute;
                left: 0;
                top: 0;
            }
        }

        .card-right {
            position: relative;
            flex: none;
            width: 56.4vw;
            height: calc(@card-width * 9 / 16);
            float: right;

            .card-ellipsis {
                overflow: hidden;
                text-overflow: ellipsis;
                white-space: nowrap;
            }

            .card-title {
                padding: 0 0 9px 7px;
                font-weight: 500;
                line-height: 15px;
                font-size: 14px;
                color: #333;
                vertical-align: middle;
            }

            .card-desc {
                padding: 6px 0 6px 7px;
                line-height: 15px;
                font-size: 12px;
                color: #666;
                vertical-align: middle;
            }

            .card-bottom {
                padding: 9px 0 0 7px;
                line-height: 15px;

                &:after {
                    clear: both;
                    content: "";
                    display: table;
                }

                .info {
                    color: #999;
                    font-size: 12px;
                    float: left;
                }

                .price {
                    font-size: 12px;
                    float: right;
                }
            }
        }

    }
</style>
