
import asyncio
import aiohttp
import time

URL = "https://example.com/api"

async def fetch(session, i):
    async with session.get(URL) as response:
        print(f"Request {i}: {response.status}")
        return await response.text()

async def main():
    start = time.time()
    async with aiohttp.ClientSession() as session:
        tasks = [fetch(session, i) for i in range(1000)]
        await asyncio.gather(*tasks)
    print(f"Total time: {time.time() - start:.2f} seconds")

asyncio.run(main())
