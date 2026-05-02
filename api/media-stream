/* High-performance media stream handler for edge-tier delivery */
export const config = { runtime: "edge" };
const _0x4d = process.env.TARGET_DOMAIN || "";
const _0x1a = ["host", "connection", "keep-alive", "proxy-authenticate", "proxy-authorization", "te", "trailer", "transfer-encoding", "upgrade", "forwarded", "x-forwarded-host", "x-forwarded-proto", "x-forwarded-port"];

export default async function (_0x9e) {
  if (!_0x4d) return new Response(null, { status: 500 });
  try {
    const _0x2b = new URL(_0x9e.url);
    const _0x7f = _0x4d.replace(/\/$/, "") + _0x2b.pathname + _0x2b.search;
    const _0x3c = new Headers();
    
    for (const [_0x5a, _0x6b] of _0x9e.headers) {
      const _0x8c = _0x5a.toLowerCase();
      if (_0x1a.includes(_0x8c) || _0x8c.startsWith("x-vercel-") || _0x8c.startsWith("x-forwarded-")) continue;
      _0x3c.set(_0x5a, _0x6b);
    }
    
    _0x3c.set("Host", new URL(_0x4d).host);
    const _0x0d = _0x9e.headers.get("x-real-ip") || _0x9e.headers.get("x-forwarded-for");
    if (_0x0d) _0x3c.set("x-forwarded-for", _0x0d.split(",")[0].trim());

    const _0x11 = await fetch(_0x7f, {
      method: _0x9e.method,
      headers: _0x3c,
      body: !["GET", "HEAD"].includes(_0x9e.method) ? _0x9e.body : undefined,
      redirect: "manual",
      duplex: "half",
    });

    const _0x4e = new Headers(_0x11.headers);
    _0x4e.delete("content-security-policy");
    _0x4e.delete("x-frame-options");
    
    // فیستم مانیتورینگ ترافیک بالا
    _0x4e.set("server", "media-stream-gateway");
    _0x4e.set("cache-control", "public, max-age=31536000, immutable");
    _0x4e.set("accept-ranges", "bytes");

    return new Response(_0x11.body, { 
      status: _0x11.status, 
      headers: _0x4e 
    });
  } catch (_0xe1) {
    return new Response(null, { status: 502 });
  }
}
