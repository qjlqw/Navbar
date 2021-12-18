//获取小程序头部的信息
getScreenHeight() {
      Taro.getSystemInfo({
        success: (result) => {
          this.$store.state.SystemInfo = result
          let { top } = result.safeArea
          if (top > 20) {
            this.$store.state.top = 24
          }
        },
      })
    },
