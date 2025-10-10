### 1. 安装

```shell
pnpm i unocss
pnpm i @unocss/reset  # 样式重置表
pnpm i @iconify/json  # 图表预设
pnpm i @vueuse/core   # 深色模式
```

### 2. 初始化

##### 1. vite.config.js 中

```js
import { defineConfig } from 'vite';
import vue from '@vitejs/plugin-vue';
import unocss from 'unocss/vite';

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [vue(), unocss()],
});
```

##### 2. main.js

```js
import { createApp } from 'vue';

/** 重置样式 这里引入自定义的重置样式也可 */
import '@unocss/reset/tailwind.css';
/**
 *  项目内的样式，
 *  注意：最好放在重置样式后，uno.css前
 */
import './style.css';
/** 引入uno.css，不引入不生效 */
import 'uno.css';

import App from './App.vue';

createApp(App).mount('#app');
```

##### 3. 创建 style.css

```css
:root {
  --primary-color: #316c72;
  --dark-bg: #18181c;
}

html {
  font-size: 4px; // * 方便unocss计算：1单位 = 0.25rem = 1px
}

body {
  font-size: 16px;
}

html,
body,
#app {
  height: 100%;
  margin: 0;
  padding: 0;
}

html.dark {
  background: var(--dark-bg);
}
```

##### 4. 新增 unocss.config.js

```js
import {
  defineConfig,
  presetAttributify,
  presetUno,
  presetIcons,
} from 'unocss';

export default defineConfig({
  presets: [
    presetUno(),
    presetAttributify(),
    presetIcons({ scale: 1.2, warn: true }),
  ],
  // 常用的样式缩写
  shortcuts: [
    ['wh-full', 'w-full h-full'],
    ['f-c-c', 'flex justify-center items-center'],
    ['flex-col', 'flex flex-col'],
    ['text-ellipsis', 'truncate'],
    [
      'icon-btn',
      'text-16 inline-block cursor-pointer select-none opacity-75 transition duration-200 ease-in-out hover:opacity-100 hover:text-primary !outline-none',
    ],
  ],
  rules: [
    [/^bc-(.+)$/, ([, color]) => ({ 'border-color': `#${color}` })],
    [
      'card-shadow',
      {
        'box-shadow':
          '0 1px 2px -2px #00000029, 0 3px 6px #0000001f, 0 5px 12px 4px #00000017',
      },
    ],
  ],
  theme: {
    colors: {
      primary: 'var(--primary-color)',
      dark_bg: 'var(--dark-bg)',
    },
  },
});
```

### 3. 使用时注意项

##### 1.
