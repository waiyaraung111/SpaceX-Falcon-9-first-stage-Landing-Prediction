In this line:

```python
data = data[data['cores'].map(len) == 1]
```

the `.map(len)` is applying the **`len` function** to **each element in the `cores` column**, and it's doing the same for `payloads`.

------

### 🔍 What is `.map()`?

`.map()` is a **Pandas Series method** that applies a **function** to every item in the column (which is a Series).

#### In your case:

- `data['cores']` is a column of lists (each row contains a list of core objects)
- `len` is the built-in Python function that returns the length of a list

So:

```python
data['cores'].map(len)
```

Returns a new Series like:

```
0    1
1    3
2    1
...
```

You’re then filtering to keep **only those rows where the list length is exactly 1**, meaning the launch had only **1 core** (no extra boosters).

------

### ✅ Why filter this way?

SpaceX sometimes launches rockets with:

- **Multiple cores** (like Falcon Heavy with 3 boosters)
- **Multiple payloads** (e.g., 2+ satellites in one rocket)

If you're analyzing individual rocket performance (e.g., landing success, reuse), **multiple cores or payloads complicate the analysis**. So we clean the data to keep it simple — 1 core and 1 payload per row.

------

### 🔁 Same goes for payloads:

```python
data = data[data['payloads'].map(len) == 1]
```

Only keeps rows where exactly 1 payload is present.

------

