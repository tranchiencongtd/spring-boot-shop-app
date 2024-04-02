<script setup lang="ts">
import { computed, ref, defineAsyncComponent } from 'vue';
import { useRoute } from 'vue-router';
import { useStore } from 'vuex';
import { Main } from '../../../styled';
import { TopToolBox } from '../Style';
// import { CarouselStyleWraper } from '../../../uiElements/ui-elements-styled';
import Styled from 'vue3-styled-components';

const Filters = defineAsyncComponent(() => import('./overview/Filters.vue'));

const { state, dispatch } = useStore();
const searchData = computed(() => state.headerSearchData.data);
const { matched } = useRoute();
const { path } = matched[1];
const onSorting = (e: any) => {
  dispatch('sorting', e.target.value);
};
const sortDefault = ref('rate');
const innerWidth = ref(window.innerWidth);

const CarouselStyleWraper = Styled.div`
  .ant-carousel {
    padding: none;
  }  
  .ant-carousel .slick-slide {
    text-align: center;
    height: 35rem;
    line-height: 160px;
    background: #5A5F7D;
    overflow: hidden;
  }
  .ant-carousel .slick-dots li{
    width: 25px;
  }
  .ant-carousel .slick-dots li button{
    height: 5px;
  }
  .ant-carousel .slick-dots li.slick-active{
    width: 35px;
  }
  .ant-radio-group{
    margin-bottom: 16px !important;
  }
  .ant-radio-button-wrapper{
    font-size: 14px;
    height: 38px !important;
    line-height: 36px !important;
    font-weight: 600;
    color: ${({ theme }) => theme['light-color']} !important;
  }
  .ant-carousel .slick-slide h3 {
    color: #fff;
  }
`;

const CardStyleWraper = Styled.div`
  .ant-card-body {
    padding: 0 !important;
  } 
`;
</script>

<template>
  <CardStyleWraper>
    <sdCards>
      <CarouselStyleWraper>
        <a-carousel autoplay>
          <div>
            <h3>1</h3>
          </div>
          <div>
            <h3>2</h3>
          </div>
          <div>
            <h3>3</h3>
          </div>
          <div>
            <h3>4</h3>
          </div>
        </a-carousel>
      </CarouselStyleWraper>
    </sdCards>
  </CardStyleWraper>
  <Main>
    <a-row :gutter="30">
      <a-col class="product-sidebar-col" :xxl="5" :xl="7" :lg="7" :md="10" :xs="24">
        <Suspense>
          <template #default>
            <Filters />
          </template>
          <template #fallback>
            <sdCards headless>
              <a-skeleton :paragraph="{ rows: 22 }" active />
            </sdCards>
          </template>
        </Suspense>
      </a-col>
      <a-col class="product-content-col" :xxl="19" :lg="17" :md="14" :xs="24">
        <TopToolBox>
          <a-row :gutter="0">
            <a-col :xxl="7" :lg="12" :xs="24">
              <!-- <a-input-search class="home-search" placeholder="input search text" /> -->
              <a-input class="home-search" placeholder="Tìm kiếm">
                <template #prefix> <unicon name="search" class="icon-home-search"></unicon></template>
              </a-input>
            </a-col>
            <a-col :xxl="7" :lg="12" :xs="24">
              <p class="search-result">Hiển thị 1–8 of 86 kết quả</p>
            </a-col>
            <a-col :xxl="10" :xs="24">
              <div class="product-list-action d-flex justify-content-between align-items-center">
                <div class="product-list-action__tab">
                  <span class="toolbox-menu-title"> Sắp xếp:</span>
                  <a-radio-group @change="onSorting" v-model:value="sortDefault">
                    <a-radio-button value="rate">Đánh giá cao</a-radio-button>
                    <a-radio-button value="popular">Phổ biến</a-radio-button>
                    <a-radio-button value="time">Mới nhất</a-radio-button>
                    <a-radio-button value="price">Giá</a-radio-button>
                  </a-radio-group>
                </div>

                <div
                  v-if="(innerWidth <= 991 && innerWidth >= 768) || innerWidth > 575"
                  class="product-list-action__viewmode"
                >
                  <router-link :to="`${path}product/grid`">
                    <unicon name="apps" width="16"></unicon>
                  </router-link>
                  <router-link :to="`${path}product/list`">
                    <unicon name="list-ul" width="16"></unicon>
                  </router-link>
                </div>
              </div>
            </a-col>
          </a-row>
        </TopToolBox>
        <router-view name="grid"></router-view>
      </a-col>
    </a-row>
  </Main>
</template>
