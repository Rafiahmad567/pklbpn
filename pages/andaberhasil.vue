<template>
  <div class="wrapper">
    <div class="content">
      <div class="container">
        <div class="content-inner">
          <h2>Anda telah berhasil</h2>
          <h3>mengisi absen</h3>
        </div>
      </div>
    </div>
    <FooterComponent />
  </div>
</template>

<style scoped>
html, body, .wrapper {
  height: 100%;
  margin: 0;
  padding: 0;
}

.wrapper {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

.content {
  flex: 1;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 20px;
}

.container {
  text-align: center;
  background-color: #f8f8f8;
  border-radius: 10px;
  width: 100%;
  max-width: 600px;
  padding: 20px;
}

.content-inner {
  margin-top: 20px;
  font-size: 20px;
  font-weight: bold;
}
</style>
