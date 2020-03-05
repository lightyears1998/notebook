# PKG

```sh
yarn global add pkg

pkg .
# 注意使用pkg能够处理的相应的Node版本，当涉及需要编译的二进制包时尤其如此。
# 等价于 `pkg package.json`
# 另一种 pkg lib/index.js --targets latest
```

并不是所有的Node版本都可以打包的，这跟<https://github.com/zeit/pkg-fetch/releases>中的版本有关。
