# Advanced Web Exercises - Solutions
**Module:** Advanced Web Development  
**Evening Session**

---

## Exercise 1

> Consider the tasks given in your notes on the last slide: Chapter 4 and Chapter 5.

This exercise refers to the practical tasks covered in your lecture notes for Chapters 4 and 5. Please review the relevant slides and apply the concepts practiced in class (typically covering JavaScript functions, DOM manipulation, PHP basics, and form handling as covered in those chapters).

---

## Exercise 2 - Cafeteria Meal Cost Calculator (JavaScript)

**Task:** Prompt for meal price and quantity, calculate total, apply 5% discount if total > 20,000 RWF, display final amount.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Cafeteria Calculator</title>
</head>
<body>

<script>
  // 1. Prompt user for inputs
  var price    = parseFloat(prompt("Enter the price of the meal (RWF):"));
  var quantity = parseInt(prompt("Enter the quantity purchased:"));

  // 2. Calculate total cost
  var total = price * quantity;

  // 3. Check discount eligibility
  var discount    = 0;
  var finalAmount = total;

  if (total > 20000) {
    discount    = total * 0.05;
    finalAmount = total - discount;
    alert(
      "Total: " + total + " RWF\n" +
      "Discount (5%): " + discount + " RWF\n" +
      "Final Amount to Pay: " + finalAmount + " RWF"
    );
  } else {
    // 4. Display final amount — no discount
    alert(
      "Total: " + total + " RWF\n" +
      "No discount applied.\n" +
      "Final Amount to Pay: " + finalAmount + " RWF"
    );
  }
</script>

</body>
</html>
```

**How it works:**
- `prompt()` captures the meal price and quantity from the user.
- The total is computed by multiplying price × quantity.
- An `if/else` checks whether the total exceeds 20,000 RWF.
- If yes, 5% is deducted; either way `alert()` displays the final amount.

---

## Exercise 3 - Student Records Table (React JS)

**Task:** Recreate the Student Records table with ID, Names, Address, Phone, and Edit/Delete action buttons.

```jsx
import { useState } from "react";

const initialStudents = [
  { id: 5, name: "HKIZIMANA JAMES", address: "KIGALI",   phone: "0784593955" },
  { id: 7, name: "UWIMANA MARRY",   address: "MUHANGA",  phone: "0789665613" },
  { id: 8, name: "KABERA PETER",    address: "KABEZA",   phone: "0789665613" },
];

export default function StudentRecords() {
  const [students, setStudents] = useState(initialStudents);

  const handleDelete = (id) => {
    setStudents(students.filter((s) => s.id !== id));
  };

  const handleEdit = (id) => {
    const student = students.find((s) => s.id === id);
    const newName = prompt("Edit name:", student.name);
    if (newName) {
      setStudents(students.map((s) => s.id === id ? { ...s, name: newName } : s));
    }
  };

  const handleAdd = () => {
    const name    = prompt("Enter name:");
    const address = prompt("Enter address:");
    const phone   = prompt("Enter phone:");
    if (name && address && phone) {
      const newId = Math.max(...students.map((s) => s.id)) + 1;
      setStudents([...students, { id: newId, name, address, phone }]);
    }
  };

  return (
    <div style={styles.wrapper}>
      {/* Header */}
      <div style={styles.header}>
        <span style={styles.icon}>🏫</span>
        <h2 style={styles.title}>Student Records</h2>
      </div>

      {/* Add button */}
      <div style={styles.addRow}>
        <button onClick={handleAdd} style={styles.addBtn}>+ Add New Record</button>
      </div>

      {/* Table */}
      <table style={styles.table}>
        <thead>
          <tr style={styles.thead}>
            <th style={styles.th}>ID</th>
            <th style={styles.th}>NAMES</th>
            <th style={styles.th}>ADDRESS</th>
            <th style={styles.th}>PHONE</th>
            <th style={styles.th}>ACTIONS</th>
          </tr>
        </thead>
        <tbody>
          {students.map((s) => (
            <tr key={s.id} style={styles.tr}>
              <td style={styles.td}>{s.id}</td>
              <td style={styles.td}>{s.name}</td>
              <td style={styles.td}>{s.address}</td>
              <td style={styles.td}>{s.phone}</td>
              <td style={styles.td}>
                <button onClick={() => handleEdit(s.id)}   style={styles.editBtn}>Edit</button>
                <button onClick={() => handleDelete(s.id)} style={styles.deleteBtn}>Delete</button>
              </td>
            </tr>
          ))}
        </tbody>
      </table>
    </div>
  );
}

const styles = {
  wrapper: {
    maxWidth: "700px",
    margin: "40px auto",
    background: "#fff",
    borderRadius: "8px",
    boxShadow: "0 2px 10px rgba(0,0,0,0.1)",
    padding: "24px",
    fontFamily: "Arial, sans-serif",
  },
  header: {
    display: "flex",
    alignItems: "center",
    justifyContent: "center",
    gap: "10px",
    marginBottom: "16px",
  },
  icon:  { fontSize: "2rem" },
  title: { fontSize: "1.4rem", fontWeight: "bold", margin: 0 },
  addRow: { display: "flex", justifyContent: "flex-end", marginBottom: "12px" },
  addBtn: {
    background: "#2563eb",
    color: "#fff",
    border: "none",
    borderRadius: "4px",
    padding: "8px 14px",
    cursor: "pointer",
    fontSize: "0.875rem",
  },
  table:  { width: "100%", borderCollapse: "collapse" },
  thead:  { background: "#2563eb" },
  th: {
    color: "#fff",
    padding: "10px 12px",
    textAlign: "left",
    fontSize: "0.85rem",
    fontWeight: "bold",
  },
  tr: { borderBottom: "1px solid #e5e7eb" },
  td: { padding: "10px 12px", fontSize: "0.875rem", color: "#374151" },
  editBtn: {
    background: "#16a34a",
    color: "#fff",
    border: "none",
    borderRadius: "4px",
    padding: "5px 10px",
    marginRight: "6px",
    cursor: "pointer",
    fontSize: "0.8rem",
  },
  deleteBtn: {
    background: "#dc2626",
    color: "#fff",
    border: "none",
    borderRadius: "4px",
    padding: "5px 10px",
    cursor: "pointer",
    fontSize: "0.8rem",
  },
};
```

---

## Exercise 4 - Login Form (React JS)

**Task:** Recreate the login form with Username, Password, Forgot Password link, Login button, and Register link.

```jsx
import { useState } from "react";

export default function LoginForm() {
  const [username, setUsername] = useState("");
  const [password, setPassword] = useState("");

  const handleSubmit = (e) => {
    e.preventDefault();
    alert(`Logging in as: ${username}`);
  };

  return (
    <div style={styles.page}>
      <div style={styles.card}>
        <h2 style={styles.title}>Login</h2>

        <form onSubmit={handleSubmit} style={styles.form}>
          {/* Username */}
          <div style={styles.inputWrapper}>
            <span style={styles.inputIcon}>👤</span>
            <input
              type="text"
              placeholder="Username"
              value={username}
              onChange={(e) => setUsername(e.target.value)}
              style={styles.input}
              required
            />
          </div>

          {/* Password */}
          <div style={styles.inputWrapper}>
            <span style={styles.inputIcon}>🔒</span>
            <input
              type="password"
              placeholder="Password"
              value={password}
              onChange={(e) => setPassword(e.target.value)}
              style={styles.input}
              required
            />
          </div>

          {/* Forgot password */}
          <div style={styles.forgotRow}>
            <a href="#" style={styles.forgotLink}>Forgot Password?</a>
          </div>

          {/* Submit */}
          <button type="submit" style={styles.loginBtn}>Login</button>
        </form>

        {/* Register link */}
        <p style={styles.registerText}>
          Don't have an account?{" "}
          <a href="#" style={styles.registerLink}>Register Here</a>
        </p>
      </div>
    </div>
  );
}

const styles = {
  page: {
    minHeight: "100vh",
    display: "flex",
    alignItems: "center",
    justifyContent: "center",
    background: "#f3f4f6",
    fontFamily: "Arial, sans-serif",
  },
  card: {
    background: "#fff",
    borderRadius: "8px",
    boxShadow: "0 2px 12px rgba(0,0,0,0.1)",
    padding: "36px 32px",
    width: "100%",
    maxWidth: "380px",
  },
  title: {
    textAlign: "center",
    fontSize: "1.5rem",
    fontWeight: "bold",
    marginBottom: "24px",
    color: "#111",
  },
  form:         { display: "flex", flexDirection: "column", gap: "14px" },
  inputWrapper: {
    display: "flex",
    alignItems: "center",
    border: "1px solid #d1d5db",
    borderRadius: "6px",
    padding: "10px 12px",
    gap: "10px",
  },
  inputIcon: { fontSize: "1rem" },
  input: {
    border: "none",
    outline: "none",
    width: "100%",
    fontSize: "0.9rem",
    color: "#374151",
    background: "transparent",
  },
  forgotRow:  { display: "flex", justifyContent: "flex-end" },
  forgotLink: { fontSize: "0.85rem", color: "#2563eb", textDecoration: "none" },
  loginBtn: {
    background: "#2563eb",
    color: "#fff",
    border: "none",
    borderRadius: "6px",
    padding: "12px",
    fontSize: "1rem",
    fontWeight: "bold",
    cursor: "pointer",
    marginTop: "4px",
  },
  registerText: {
    textAlign: "center",
    fontSize: "0.85rem",
    color: "#6b7280",
    marginTop: "20px",
  },
  registerLink: { color: "#2563eb", fontWeight: "bold", textDecoration: "none" },
};
```

---

## Exercise 5 - Loan Eligibility Checker (PHP)

**Task:** Capture monthly income and employment status from a form, then print eligibility result to the browser.

### `index.html` - The Form

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Rwanda Smart Banking — Loan Eligibility</title>
  <style>
    body { font-family: Arial, sans-serif; max-width: 420px; margin: 60px auto; }
    h2   { text-align: center; }
    label  { display: block; margin-top: 14px; font-size: 0.9rem; }
    input, select {
      width: 100%; padding: 9px; margin-top: 4px;
      border: 1px solid #ccc; border-radius: 4px; font-size: 0.9rem;
    }
    button {
      width: 100%; margin-top: 20px; padding: 10px;
      background: #2563eb; color: #fff; border: none;
      border-radius: 4px; font-size: 1rem; cursor: pointer;
    }
  </style>
</head>
<body>
  <h2>Loan Eligibility Check</h2>
  <form action="loan.php" method="POST">
    <label>Monthly Income (RWF)
      <input type="number" name="income" placeholder="e.g. 350000" required />
    </label>
    <label>Employment Status
      <select name="employment">
        <option value="Permanent">Permanent</option>
        <option value="Contract">Contract</option>
        <option value="Unemployed">Unemployed</option>
      </select>
    </label>
    <button type="submit">Check Eligibility</button>
  </form>
</body>
</html>
```

### `loan.php` - The Logic

```php
<?php
  $income     = (float) $_POST['income'];
  $employment = $_POST['employment'];

  // Determine result
  if ($income >= 300000 && $employment === "Permanent") {
      $result = "✅ Eligible for loan.";
      $color  = "green";
  } elseif ($income >= 300000 && $employment === "Contract") {
      $result = "⚠️ Eligible with conditions.";
      $color  = "orange";
  } else {
      $result = "❌ Not eligible for loan.";
      $color  = "red";
  }
?>
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Loan Result</title>
  <style>
    body   { font-family: Arial, sans-serif; max-width: 420px; margin: 60px auto; }
    .result { padding: 16px; border-radius: 6px; font-size: 1.1rem; font-weight: bold;
              border: 1px solid <?php echo $color; ?>; color: <?php echo $color; ?>; }
    a { display: block; margin-top: 16px; color: #2563eb; }
  </style>
</head>
<body>
  <h2>Loan Eligibility Result</h2>
  <p>Income: <strong><?php echo number_format($income); ?> RWF</strong></p>
  <p>Status: <strong><?php echo htmlspecialchars($employment); ?></strong></p>
  <div class="result"><?php echo $result; ?></div>
  <a href="index.html">← Check Again</a>
</body>
</html>
```

---

## Exercise 6 - Bus Fare Calculator (PHP)

**Task:** Capture travel distance from a form, compute the fare by distance range, and print the result to the browser.

### `index.html` - The Form

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Rwanda Smart Transport — Fare Calculator</title>
  <style>
    body { font-family: Arial, sans-serif; max-width: 400px; margin: 60px auto; }
    h2   { text-align: center; }
    label  { display: block; margin-top: 14px; font-size: 0.9rem; }
    input  {
      width: 100%; padding: 9px; margin-top: 4px;
      border: 1px solid #ccc; border-radius: 4px; font-size: 0.9rem;
    }
    button {
      width: 100%; margin-top: 20px; padding: 10px;
      background: #16a34a; color: #fff; border: none;
      border-radius: 4px; font-size: 1rem; cursor: pointer;
    }
  </style>
</head>
<body>
  <h2>Bus Fare Calculator</h2>
  <form action="fare.php" method="POST">
    <label>Travel Distance (km)
      <input type="number" name="distance" min="1" placeholder="e.g. 12" required />
    </label>
    <button type="submit">Calculate Fare</button>
  </form>
</body>
</html>
```

### `fare.php` - The Logic

```php
<?php
  $distance = (int) $_POST['distance'];

  // Determine fare based on distance range
  if ($distance >= 0 && $distance <= 5) {
      $fare    = 300;
      $message = "Short trip (0–5 km): flat rate applies.";
  } elseif ($distance <= 15) {
      $fare    = 500;
      $message = "Medium trip (6–15 km): standard fare.";
  } elseif ($distance <= 30) {
      $fare    = 800;
      $message = "Long trip (16–30 km): extended fare.";
  } else {
      $fare    = 1200;
      $message = "Very long trip (30+ km): maximum fare.";
  }
?>
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Fare Result</title>
  <style>
    body { font-family: Arial, sans-serif; max-width: 400px; margin: 60px auto; }
    .box {
      border: 1px solid #16a34a; border-radius: 6px;
      padding: 16px; color: #15803d; font-weight: bold; font-size: 1rem;
    }
    a { display: block; margin-top: 16px; color: #2563eb; }
  </style>
</head>
<body>
  <h2>Fare Calculation Result</h2>
  <p>Distance entered: <strong><?php echo $distance; ?> km</strong></p>
  <div class="box">
    Calculated Fare: <?php echo $fare; ?> RWF
  </div>
  <p><?php echo $message; ?></p>
  <a href="index.html">← Calculate Another</a>
</body>
</html>
```

---

*Good luck with your exam! 🎓*



