# 💻 Vantex AI Architecture Snippets

## 1. Governance Modal Component
*Demonstrates the modular information architecture using React/Next.js*

```tsx
<InfoModal
  isOpen={isDisclaimerOpen}
  onClose={() => setIsDisclaimerOpen(false)}
  title="VANTEX AI | INTEGRATED DECENTRALIZED GOVERNANCE DISCLOSURE (V.1.0)"
  icon="scale"
>
  <div className="space-y-6 text-white/80">
    <section>
      <h3 className="text-white font-semibold text-lg mb-2">1.1. Agentic Delegation</h3>
      <p>Vantex AI introduces a radical paradigm shift in decentralized decision-making...</p>
    </section>
  </div>
</InfoModal>
```

## 2. Footer Social Integration
*Clean, semantic HTML5 structure with optimized SVG assets*

```tsx
<Link
  href="https://x.com/Vantex_AI"
  className="text-white/70 hover:text-white transition-colors"
  aria-label="X (Twitter)"
>
  <svg className="w-6 h-6" fill="currentColor" viewBox="0 0 24 24">
    <path d="M18.244 2.25h3.308l-7.227 8.26 8.502 11.24H16.17l-5.214-6.817L4.99 21.75H1.68l7.73-8.835L1.254 2.25H8.08l4.713 6.231zm-1.161 17.52h1.833L7.084 4.126H5.117z" />
  </svg>
</Link>
```

## 3. Configuration & Security
*Next.js Security Headers & Strict Mode*

```typescript
const nextConfig: NextConfig = {
  typescript: {
    // Strict type validation enabled for production safety
    ignoreBuildErrors: false, 
  },
  images: {
    remotePatterns: [
      {
        protocol: 'https',
        hostname: 'ik.imagekit.io', // Trusted CDN
      }
    ]
  }
};
```
