# Custom Hooks

## 1. What are Custom Hooks?

- Refers to hooks customized by developers themselves
- Can **extract repeated logic into functions for reuse** using this

### (1) When to Use Custom Hooks

- When fetching multiple URLs
- When you want repeated logic like state changes by multiple inputs to work in the same function

### (2) Advantages of Custom Hooks

- **Reuse** of state management logic is possible
- Can implement the same logic with **less code** compared to class components
- Has the advantage of being **more clear** because it's written functionally (e.g. `useSomething`)

<br/>

## 2. Custom Hooks Usage Example

- For example, if there are components like below:

  ```javascript
  // FriendStatus: Component that returns whether friend is online or offline
  function FriendStatus(props) {
    const [isOnline, setIsOnline] = useState(null);
    useEffect(() => {
      function handleStatusChange(status) {
        setIsOnline(status.isOnline);
      }
      ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
      return () => {
        ChatAPI.unsubscribeFromFriendStatus(
          props.friend.id,
          handleStatusChange
        );
      };
    });

    if (isOnline === null) {
      return 'Loading...';
    }
    return isOnline ? 'Online' : 'Offline';
  }

  // FriendListItem: Component that displays friend in green when online
  function FriendListItem(props) {
    const [isOnline, setIsOnline] = useState(null);
    useEffect(() => {
      function handleStatusChange(status) {
        setIsOnline(status.isOnline);
      }
      ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
      return () => {
        ChatAPI.unsubscribeFromFriendStatus(
          props.friend.id,
          handleStatusChange
        );
      };
    });

    return (
      <li style={{ color: isOnline ? 'green' : 'black' }}>
        {props.friend.name}
      </li>
    );
  }
  ```

- **Separate logic used identically in both components to use function `useFriendStatus`** → When defining Custom Hook, the following rules are needed:

  - (1) When defining Custom Hook, **add `use` before function name**
  - (2) In most cases, **place Custom Hook in hooks directory within project**
  - (3) When making into Custom Hook, function **should not be conditional function**. In other words, returned value should not be conditional. Therefore, this `useFriendStatus` Hook returns online status as boolean type.

- Custom Hook made this way can be written using React built-in Hooks like `useState` inside the Hook
- Cannot call React built-in Hooks inside regular functions, but possible in Custom Hooks

- Code applying `useFriendStatus` Hook to both components

  ```javascript
  function FriendStatus(props) {
    const isOnline = useFriendStatus(props.friend.id); // Apply useFriendStatus Hook

    if (isOnline === null) {
      return 'Loading...';
    }
    return isOnline ? 'Online' : 'Offline';
  }

  function FriendListItem(props) {
    const isOnline = useFriendStatus(props.friend.id);

    return (
      <li style={{ color: isOnline ? 'green' : 'black' }}>
        {props.friend.name}
      </li>
    );
  }
  ```

- Because logic was separated to make Custom Hook, both components can be checked more intuitively
- However, just because the same Custom Hook was used doesn't mean the two components share the same state. They just **share logic, but state is defined independently within each component**
