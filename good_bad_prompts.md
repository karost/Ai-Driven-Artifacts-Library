### **Example of Good vs. Bad Prompt**

#### **Scenario**: Generate a Next.js page that fetches and displays a list of blog posts from an API.

---

### **Bad Prompt (Lazy Prompt)**

**Prompt:**
```
Create a Next.js page to fetch and display blog posts.
```

**Outcome:**
```javascript
import React from 'react';

const BlogPage = () => {
  return (
    <div>
      <h1>Blog Posts</h1>
      <p>Blog content will go here.</p>
    </div>
  );
};

export default BlogPage;
```

---

### **Good Prompt (Structured with Templates)**

**Prompt:**
```
You are an expert in React and Next.js development. 

Task:
Create a Next.js page that fetches and displays a list of blog posts from a REST API. Use the `getServerSideProps` function for data fetching. Include the following:
- A loading state while the data is being fetched.
- Graceful error handling.
- Display each blog post's title and description.

Output format:
1. Fully functional Next.js page.
2. Include comments explaining each part of the code.
3. Use modern React and Next.js conventions.

Example:
Input: Create a Next.js page to fetch and display user data.
Output:
```javascript
import React from 'react';
import axios from 'axios';

export async function getServerSideProps() {
  try {
    const { data } = await axios.get('https://api.example.com/users');
    return { props: { users: data } };
  } catch (error) {
    return { props: { users: [], error: error.message } };
  }
}

const UsersPage = ({ users, error }) => {
  if (error) return <p>Error: {error}</p>;

  return (
    <div>
      <h1>User List</h1>
      {users.length > 0 ? (
        <ul>
          {users.map((user) => (
            <li key={user.id}>{user.name}</li>
          ))}
        </ul>
      ) : (
        <p>No users found.</p>
      )}
    </div>
  );
};

export default UsersPage;
```

Your turn:
Create a Next.js page for the blog posts use case.
```

**Outcome:**
```javascript
import React from 'react';
import axios from 'axios';

export async function getServerSideProps() {
  try {
    const { data } = await axios.get('https://api.example.com/blog-posts');
    return { props: { posts: data } };
  } catch (error) {
    return { props: { posts: [], error: error.message } };
  }
}

const BlogPage = ({ posts, error }) => {
  if (error) return <p>Error: {error}</p>;

  return (
    <div>
      <h1>Blog Posts</h1>
      {posts.length > 0 ? (
        <ul>
          {posts.map((post) => (
            <li key={post.id}>
              <h2>{post.title}</h2>
              <p>{post.description}</p>
            </li>
          ))}
        </ul>
      ) : (
        <p>No blog posts found.</p>
      )}
    </div>
  );
};

export default BlogPage;
```

---

### **Analysis of the Outcomes**

| **Criteria**                | **Bad Prompt**                                              | **Good Prompt**                                              |
|-----------------------------|------------------------------------------------------------|-------------------------------------------------------------|
| **Clarity**                 | Lacks specifics on data fetching, error handling, or output structure. | Clear and detailed instructions guide the desired behavior. |
| **Code Quality**            | Output is generic and incomplete.                          | Output is production-ready with error handling, comments, and best practices. |
| **Functionality**           | Static placeholder; no dynamic behavior.                   | Fully dynamic page with API integration.                    |
| **Error Handling**          | None.                                                      | Graceful error handling included.                           |
| **Learning Opportunity**    | Offers little guidance or improvement for the user.         | Demonstrates best practices with clear explanations.         |
| **Reusability**             | Hard to adapt to similar use cases.                        | Template-based and reusable for other scenarios.            |

---

### **Key Takeaways**

1. **Bad Prompts Lead to Poor Results**:
   - The model doesn’t have enough context or instructions to generate useful or functional output.
   - Generic or incomplete code wastes time as you have to rewrite or debug.

2. **Good Prompts Empower the Model**:
   - Detailed instructions set the stage for high-quality, context-aware output.
   - Examples act as a learning guide and ensure the output matches your expectations.

3. **Templates Encourage Reusability**:
   - Good prompts can serve as a foundation for future requests, reducing iteration time.
   - By embedding examples, you help the model understand your preferred style and standards.

---

### **Pro Tip: Template for Good Prompts**

**System Prompt:**
```
You are a highly skilled React and Next.js developer. Always write production-ready, modern code with detailed comments.
```

**User Prompt Template:**
```
Task:
Describe the specific use case and requirements (e.g., "Fetch and display blog posts from an API.").

Instructions:
- Explain how to handle data fetching (e.g., `getServerSideProps`, `getStaticProps`).
- Mention any additional functionality (e.g., error handling, loading states).
- Specify the expected output format (e.g., "Fully functional Next.js page with comments explaining the code").

Examples:
Provide a relevant example for the task with a clear input-output format.

Input:
Describe the sample task.

Output:
Show the expected output format.
``` 

Following this approach will consistently produce higher-quality results, save time, and enhance your interaction with LLMs.
