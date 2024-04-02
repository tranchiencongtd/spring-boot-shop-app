<template>
  <div>
    <Main>
      <ErrorWrapper>
        <img :src="`/src/assets/img/pages/404.svg`" alt="404" />
        <sdHeading class="error-text" as="h3"> 404 </sdHeading>
        <p>Trang bạn tìm kiếm không tồn tại!</p>
        <router-link to="/">
          <sdButton size="default" type="primary" to="/"> Trang chủ </sdButton>
        </router-link>
      </ErrorWrapper>
    </Main>
  </div>
</template>

<script setup lang="ts">
import { Main } from '../styled';
import { ErrorWrapper } from './style';
</script>
