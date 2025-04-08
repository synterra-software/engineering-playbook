# Libraries Usage Standards

## General Approach

* Prefer established npm libraries over custom solutions
* Only build custom implementations when there are strong requirements that can't be met by existing libraries
* Consider maintenance burden, security, and community support when selecting libraries

```tsx
// ✅ Good - Using established library
import { format } from 'date-fns';
const formattedDate = format(new Date(), 'yyyy-MM-dd');

// ❌ Bad - Reinventing the wheel
const formatDate = (date) => {
  const year = date.getFullYear();
  const month = String(date.getMonth() + 1).padStart(2, '0');
  const day = String(date.getDate()).padStart(2, '0');
  return `${year}-${month}-${day}`;
};
```

## Modal Components

* Always use ebay-nice-modal for all modal implementations
* Never create modals inline or from scratch

```tsx
// ✅ Good - Using ebay-nice-modal
import { create } from 'ebay-nice-modal';

const ConfirmDialog = create(({ message }) => (
  <div>
    <h2>Confirm</h2>
    <p>{message}</p>
    <button onClick={() => ConfirmDialog.hide()}>Cancel</button>
    <button onClick={() => ConfirmDialog.resolve(true)}>Confirm</button>
  </div>
));

// Usage: await ConfirmDialog.show({ message: "Are you sure?" });
```

## Form Handling

* Always use react-hook-form for forms, even for single field forms
* Exception: Simple search components that will never require validation
* Take advantage of built-in validation and error handling

```tsx
// ✅ Good - Using react-hook-form even for simple forms
import { useForm } from 'react-hook-form';

const EmailSubscribe = () => {
  const { register, handleSubmit, errors } = useForm();
  
  const onSubmit = (data) => {
    subscribeUser(data.email);
  };
  
  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <input 
        {...register('email', { 
          required: 'Email is required',
          pattern: {
            value: /^[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,}$/i,
            message: 'Invalid email address'
          }
        })}
      />
      {errors.email && <span>{errors.email.message}</span>}
      <button type="submit">Subscribe</button>
    </form>
  );
};

// ✅ Acceptable exception - Simple search with no validation needs
const SearchBox = () => {
  const [query, setQuery] = useState('');
  
  const handleSearch = (e) => {
    e.preventDefault();
    performSearch(query);
  };
  
  return (
    <form onSubmit={handleSearch}>
      <input 
        value={query}
        onChange={(e) => setQuery(e.target.value)}
        placeholder="Search..."
      />
      <button type="submit">Search</button>
    </form>
  );
};
```

## Recommended Libraries by Category

### State Management
* Use Zustand with Immer for state management
* Structure stores by feature or domain

```tsx
// ✅ Good - Using Zustand with Immer
import create from 'zustand';
import { immer } from 'zustand/middleware/immer';

const useUserStore = create(immer((set) => ({
  users: [],
  loading: false,
  fetchUsers: async () => {
    set((state) => { state.loading = true });
    // Fetch logic...
  }
})));
```

### Data Fetching
* Use axios for API requests
* Use React Query for data fetching and caching

```tsx
// ✅ Good - Using axios with React Query
import axios from 'axios';
import { useQuery } from 'react-query';

const fetchUsers = () => axios.get('/api/users').then(res => res.data);
const useUsers = () => useQuery('users', fetchUsers);
```

### CSS Styling
* Use Tailwind CSS for all styling
* Follow the utility-first approach

```tsx
// ✅ Good - Using Tailwind CSS
const Button = ({ children, primary }) => (
  <button 
    className={`
      px-4 py-2 
      rounded 
      ${primary ? 'bg-blue-500 text-white' : 'bg-gray-200 text-gray-800'}
    `}
  >
    {children}
  </button>
);
```