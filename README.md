# Next.js App Router Course - Starter

Run `pnpm i` to install the project's packages.

Followed by `pnpm dev` to start the development server.

`pnpm dev` starts your Next.js development server on `port 3000`

---

## What's in this Course

### Styling

When you use create-next-app to start a new project, Next.js will ask if you want to use Tailwind. If you select `yes`, **Next.js** will automatically install the necessary packages and configure **Tailwind** in your application.

**Tailwind** and **CSS** modules are the two most common ways of styling Next.js applications.

/app/ui/home.module.css

```css
.shape {
  height: 0;
  width: 0;
  border-bottom: 30px solid black;
  border-left: 20px solid transparent;
  border-right: 20px solid transparent;
}
```

/app/page.tsx

```typescript


import AcmeLogo from '@/app/ui/acme-logo';
import { ArrowRightIcon } from '@heroicons/react/24/outline';
import Link from 'next/link';
import styles from '@/app/ui/home.module.css';

export default function Page() {
  return (
    <main className="flex min-h-screen flex-col p-6">
      <div className={styles.shape} />
    // ...
  )
}
```

`clsx` is a library that lets you toggle class names easily.

/app/ui/invoices/status.tsx

```typescript


import clsx from 'clsx';

export default function InvoiceStatus({ status }: { status: string }) {
  return (
    <span
      className={clsx(
        'inline-flex items-center rounded-full px-2 py-1 text-sm',
        {
          'bg-gray-100 text-gray-500': status === 'pending',
          'bg-green-500 text-white': status === 'paid',
        },
      )}
    >
    // ...
)}

```

> Take a look at the [CSS documentation](https://nextjs.org/docs/app/getting-started/css) for more information.

### Fonts

**Next.js** automatically optimizes fonts in the application when you use the next/font module. It downloads font files at build time and hosts them with your other static assets. This means when a user visits your application, there are no additional network requests for fonts which would impact performance.

/app/iu / fonts.ts;

```typescript
import { Inter, Lusitana } from "next/font/google";

export const inter = Inter({ subsets: ["latin"] });

export const lusitana = Lusitana({
  weight: ["400", "700"],
  subsets: ["latin"],
});
```

/app/layout.tsx;

```tsx
import "@/app/ui/global.css";
import { inter } from "@/app/ui/fonts";

export default function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <html lang="en">
      <body className={`${inter.className} antialiased`}>{children}</body>
    </html>
  );
}
```

### Images

Instead of manually implementing these optimizations, you can use the next/image component to automatically optimize your images.

**The `<Image>` component**
The `<Image>` Component is an extension of the HTML `<img>` tag, and comes with automatic image optimization, such as:

- Preventing layout shift automatically when images are loading.
- Resizing images to avoid shipping large images to devices with a smaller viewport.
- Lazy loading images by default (images load as they enter the viewport).
- Serving images in modern formats, like WebP and AVIF, when the browser supports it.

---

This is the starter template for the Next.js App Router Course. It contains the starting code for the dashboard application.

For more information, see the [course curriculum](https://nextjs.org/learn) on the Next.js Website.
