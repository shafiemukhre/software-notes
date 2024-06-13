## Data fetching with useEffect

```tsx
import { useEffect, useRef, useState } from "react";

const BASE_URL = "https://jsonplaceholder.typicode.com";

interface Post {
  id: number;
  title: string;
}

export default function Demo() {
  const [error, setError] = useState();
  const [isLoading, setIsLoading] = useState(false);
  const [posts, setPosts] = useState<Post[]>([]);
  const [page, setPage] = useState(0);

  const abortControllerRef = useRef<AbortController | null>(null);

  useEffect(() => {
    const fetchPosts = async () => {
      abortControllerRef.current?.abort();
      abortControllerRef.current = new AbortController();

      setIsLoading(true);

      try {
        const response = await fetch(`${BASE_URL}/posts?page=${page}`, {
          signal: abortControllerRef.current?.signal,
        });
        const posts = (await response.json()) as Post[];
        setPosts(posts);
      } catch (e: any) {
        if (e.name === "AbortError") {
          console.log("Aborted");
          return;
        }

        setError(e);
      } finally {
        setIsLoading(false);
      }
    };

    fetchPosts();
  }, [page]);

  if (error) {
    return <div>Something went wrong! Please try again.</div>;
  }

  return (
    <div className="tutorial">
      <h1 className="mb-4 text-2xl">Data Fething in React</h1>
      <button onClick={() => setPage(page + 1)}>Increase Page ({page})</button>
      {isLoading && <div>Loading...</div>}
      {!isLoading && (
        <ul>
          {posts.map((post) => {
            return <li key={post.id}>{post.title}</li>;
          })}
        </ul>
      )}
    </div>
  );
}
```

## Using fetch()

### Fetching a request

```jsx
const [jobIds, setJobIds] = useState([]);
useEffect(() => {
  fetchJobIds();
}, []);

async function fetchJobIds() {
  response = await fetch(
    `https://hacker-news.firebaseio.com/v0/jobstories.json`
  );
  data = await response.json(); // don't forget await here
  setJobIds(data);
}
```

The above is the same as below but using arrow function's chaining `.then()`.

```jsx
const [jobIds, setJobIds] = useState([]);
useEffect(() => {
  fetchJobIds();
}, []);

async function fetchJobIds() {
  data = await fetch(
    `https://hacker-news.firebaseio.com/v0/jobstories.json`
  ).then((res) => res.json());
  setJobIds(data);
}
```

### Fetching multiple requests

```jsx
  const [jobDetails, setJobDetails] = useState([])
  const URL = "https://hacker-news.firebaseio.com";

  useEffect(() => {
    if (!loading) {
      fetchJobDetails(page);
    }
  }, [page])

  async function fetchJobIds(currPage) {...}

  async function fetchJobDetails(currPage) {
    setLoading(true);
    const jobIdsForPage = await fetchJobIds(currPage);

    // highlight-start
    const JobDetailsPromise = jobIdsForPage.map((id) => (
      fetch(`${URL}/v0/item/${id}.json`).then((res) => res.json())
    ));
    const data = await Promise.all(JobDetailsPromise);
    // highlight-end

    setJobDetails([...jobDetails, ...data]);
    setLoading(false);
  }
```

The above is the same as below but using arrow function's chaining `.then()`.

```jsx
  const [jobDetails, setJobDetails] = useState([])
  const URL = "https://hacker-news.firebaseio.com";

  useEffect(() => {
    if (!loading) {
      fetchJobDetails(page);
    }
  }, [page])

  async function fetchJobIds(currPage) {...}

  async function fetchJobDetails(currPage) {
    setLoading(true);
    const jobIdsForPage = await fetchJobIds(currPage);

    // highlight-start
    const data = await Promise.all(jobIdsForPage.map((id) =>
      fetch(`${URL}/v0/item/${id}.json`).then((res) => res.json())
    ));
    // highlight-end

    setJobDetails([...jobDetails, ...data]);
    setLoading(false);
  }
```

## Prevent useEffect() from fetching multiple times

Option 1: Track a loading state to ensures that a new fetch operation doesn't start until the current one is finished. This is simpler and good enough POC for interview setting.

```jsx title="jsx"
  const [jobDetails, setJobDetails] = useState([])
  // highlight-next-line
  const [loading, setLoading] = useState(false); // loading state
  const URL = "https://hacker-news.firebaseio.com";

  useEffect(() => {
    if (!loading) {
      fetchJobDetails(page);
    }
  }, [page])

  async function fetchJobIds(currPage) {...}

  async function fetchJobDetails(currPage) {
    // highlight-next-line
    setLoading(true);
    const jobIdsForPage = await fetchJobIds(currPage);

    const data = await Promise.all(jobIdsForPage.map((id) =>
      // notice that the fetch is not in a bracket
      fetch(`${URL}/v0/item/${id}.json`).then((res) => res.json())
    ));
    setJobDetails([...jobDetails, ...data]);
    // highlight-next-line
    setLoading(false);
  }
```

Option 2: Using AbortController and loading state. This is handle edge case of when use abort a fetch request while the fetch is still ongoing. This approach ensures that any ongoing fetch operations are properly cancelled when they are no longer needed, preventing multiple fetches from happening simultaneously.

```jsx title="jsx"
const [page, setPage] = useState(0);
const [jobDetails, setJobDetails] = useState([]);
const [loading, setLoading] = useState(false); // loading fetch
const [jobIds, setJobIds] = useState([]);
const PAGE_SIZE = 6;
const URL = "https://hacker-news.firebaseio.com";

useEffect(() => {
  // highlight-start
  const controller = new AbortController();
  const { signal } = controller;
  // highlight-end

  if (!loading) {
    fetchJobDetails(page, signal);
  }

  // highlight-start
  // useEffect clean-up
  return () => {
    controller.abort();
  };
  // highlight-end
}, [page]);

// notice that the signal controller was passed to the sub-fetch request as well
async function fetchJobIds(currPage, signal) {
  // highlight-next-line
  const response = await fetch(`${URL}/v0/jobstories.json`, { signal });
  const data = await response.json();

  const start = currPage * PAGE_SIZE;
  const end = start + PAGE_SIZE;
  return data.slice(start, end);
}

async function fetchJobDetails(currPage, signal) {
  setLoading(true);
  try {
    // highlight-next-line
    const jobIdsForPage = await fetchJobIds(currPage, signal);

    const data = await Promise.all(
      jobIdsForPage.map((id) =>
        // highlight-next-line
        fetch(`${URL}/v0/item/${id}.json`, { signal }).then((res) => res.json())
      )
    );
    setJobDetails([...jobDetails, ...data]);
  } catch (error) {
    // highlight-start
    if (error.name !== "AbortError") {
      console.log("Fetch Error: ", error);
    }
    // highlight-end
  } finally {
    setLoading(false);
  }
}
```
