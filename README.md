# browser_manager

Async Playwright browser lifecycle helper. Launches a Chromium browser,
randomizes the user agent per page, and guarantees cleanup even on exception.

## Install

```bash
pip install git+https://github.com/yourname/browser_manager.git
```

## Usage

```python
from browser_manager import browser_session, new_context, new_page

async def main():
    async with browser_session() as browser:
        ctx1 = await new_context(browser)
        page1 = await new_page(ctx1)

        ctx2 = await new_context(browser)  # isolated from ctx1: no shared cookies
        page2 = await new_page(ctx2)
```

## API

| Function | Description |
|---|---|
| `browser_session(headless=True)` | Async context manager. Yields a `Browser`. Closes it and stops Playwright on exit, even on exception. |
| `new_context(browser, user_agent=None)` | Creates an isolated context: its own cookies, storage, cache. |
| `new_page(context)` | Opens a new page inside an existing context. |