[[MaterialUI|MaterialUI]] отлично интегрируется с [[Next.js|Next.js]], но для этого требуются несколько дополнительных шагов. Это связано с тем, как [[Next.js|Next.js]] обрабатывает рендеринг на стороне сервера (SSR).

## Шаги для интеграции

**Установка:**

```Shell
npm install @mui/material-nextjs @emotion/cache
```

**Конфигурация `app/layout.tsx`:**

```TypeScript
import { AppRouterCacheProvider } from '@mui/material-nextjs/v15-appRouter';


export default function RootLayout(props) {
	return (
		<html lang='en'>
			<body>
				<AppRouterCacheProvider>
				   {props.children}
				</AppRouterCacheProvider>
			</body>
		</html>
	);
}

```