# More Lessons
<details>
  <summary>Employee Reg System</summary>

  ## Mysql
  ```groovy
  -- Database creation
CREATE DATABASE IF NOT EXISTS Netbeansloginsituation;
USE Netbeansloginsituation;

-- Table creation for employee data
CREATE TABLE IF NOT EXISTS kigaliemployeesdata (
    id INT AUTO_INCREMENT PRIMARY KEY,
    company_name VARCHAR(100) NOT NULL,
    industry VARCHAR(50) NOT NULL,
    employee_name VARCHAR(100) NOT NULL,
    employee_gender VARCHAR(10) NOT NULL,
    post VARCHAR(50) NOT NULL,
    min_salary VARCHAR(50) NOT NULL,
    max_salary VARCHAR(50) NOT NULL,
    registration_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Sample data insertion (optional)
INSERT INTO kigaliemployeesdata 
(company_name, industry, employee_name, employee_gender, post, min_salary, max_salary)
VALUES
('Tech Solutions', 'IT', 'John Doe', 'Male', 'Manager', 'less than 300000 rwf', 'above 500000'),
('Green Farms', 'Farming', 'Jane Smith', 'Female', 'CEO', 'less than 500000 rwf', 'above 10000000');

-- User creation with privileges (optional)
CREATE USER IF NOT EXISTS 'emp_user'@'localhost' IDENTIFIED BY 'password123';
GRANT ALL PRIVILEGES ON loginsituation.* TO 'emp_user'@'localhost';
FLUSH PRIVILEGES;

-- Verification query
SELECT * FROM kigaliemployeesdata;
```

## Script
```groovy
package StudentRegistration;

import java.sql.*;
import javax.swing.*;
import java.awt.*;

public class Employee extends JFrame {

    private JTextField Txtcompany, Txtemployee;
    private JComboBox<String> gender, industry, maxsalary, minsalary, post;
    private JButton jButton1;

    public Employee() {
        initComponents();
    }

    private void initComponents() {
        // Colors
        Color bgColor = new Color(245, 252, 255);
        Color headerColor = new Color(0, 102, 153);
        Color labelColor = new Color(0, 51, 102);
        Color buttonColor = new Color(0, 153, 153);

        // Frame settings
        setTitle("Kigali Employee Data Entry");
        setSize(650, 600);
        setLocationRelativeTo(null);
        setDefaultCloseOperation(EXIT_ON_CLOSE);
        getContentPane().setBackground(bgColor);

        // Layout
        GridBagLayout layout = new GridBagLayout();
        GridBagConstraints c = new GridBagConstraints();
        setLayout(layout);

        // Title label
        JLabel jLabel1 = new JLabel("KIGALI EMPLOYEE DATA ENTRY FORM");
        jLabel1.setFont(new Font("Segoe UI", Font.BOLD, 26));
        jLabel1.setForeground(headerColor);
        jLabel1.setHorizontalAlignment(SwingConstants.CENTER);
        c.gridwidth = 2;
        c.insets = new Insets(20, 10, 20, 10);
        c.gridx = 0;
        c.gridy = 0;
        add(jLabel1, c);

        // Field labels and components
        String[] labels = {
            "Company Name:", "Industry:", "Employee Names:", "Gender:",
            "Post:", "Min Salary:", "Max Salary:"
        };

        Component[] fields = new Component[labels.length];

        Txtcompany = new JTextField(20);
        industry = new JComboBox<>(new String[]{"--Select--", "Farming", "IT", "Education", "Business", "Public Administration", "Politics", "Health"});
        Txtemployee = new JTextField(20);
        gender = new JComboBox<>(new String[]{"--Select--", "Male", "Female"});
        post = new JComboBox<>(new String[]{"--Select--", "CEO", "Senior Manager", "Manager", "Human Resources", "Strategic Director", "Director", "Worker Staff"});
        minsalary = new JComboBox<>(new String[]{"--Select--", "less than 100000 rwf", "less than 200000 rwf", "less than 300000 rwf", "less than 400000 rwf", "less than 500000 rwf"});
        maxsalary = new JComboBox<>(new String[]{"--Select--", "above 100000", "above 200000", "above 300000", "above 400000", "above 500000", "above 1000000"});

        fields[0] = Txtcompany;
        fields[1] = industry;
        fields[2] = Txtemployee;
        fields[3] = gender;
        fields[4] = post;
        fields[5] = minsalary;
        fields[6] = maxsalary;

        // Adding labels and fields to the form
        for (int i = 0; i < labels.length; i++) {
            JLabel lbl = new JLabel(labels[i]);
            lbl.setFont(new Font("Segoe UI", Font.PLAIN, 16));
            lbl.setForeground(labelColor);

            c.gridwidth = 1;
            c.gridx = 0;
            c.gridy = i + 1;
            c.anchor = GridBagConstraints.LINE_END;
            c.insets = new Insets(10, 10, 10, 10);
            add(lbl, c);

            c.gridx = 1;
            c.anchor = GridBagConstraints.LINE_START;
            add(fields[i], c);
        }

        // Save button
        jButton1 = new JButton("SAVE DATA");
        jButton1.setFont(new Font("Segoe UI", Font.BOLD, 18));
        jButton1.setBackground(buttonColor);
        jButton1.setForeground(Color.WHITE);
        jButton1.addActionListener(evt -> saveEmployeeData());
        c.gridx = 0;
        c.gridy = labels.length + 2;
        c.gridwidth = 2;
        c.anchor = GridBagConstraints.CENTER;
        c.insets = new Insets(25, 10, 20, 10);
        add(jButton1, c);
    }

    private void saveEmployeeData() {
        // Collect values from form
        String companyName = Txtcompany.getText().trim();
        String Industry = industry.getSelectedItem().toString();
        String employeeName = Txtemployee.getText().trim();
        String employeeGender = gender.getSelectedItem().toString();
        String Post = post.getSelectedItem().toString();
        String minSalary = minsalary.getSelectedItem().toString();
        String maxSalary = maxsalary.getSelectedItem().toString();

        // Validation checks
        if (companyName.isEmpty() || Industry.equals("--Select--") || employeeName.isEmpty()
                || employeeGender.equals("--Select--") || Post.equals("--Select--")
                || minSalary.equals("--Select--") || maxSalary.equals("--Select--")) {
            JOptionPane.showMessageDialog(this, "Please fill in all fields correctly.", "Validation Error", JOptionPane.WARNING_MESSAGE);
            return;
        }

        // Database Connection & Data Saving
        try (Connection con = DriverManager.getConnection(
                "jdbc:mysql://localhost:3306/Netbeansloginsituation?zeroDateTimeBehavior=convertToNull", "root", "");
             PreparedStatement pst = con.prepareStatement(
                     "INSERT INTO kigaliemployeesdata (company_name, industry, employee_name, employee_gender, post, min_salary, max_salary) VALUES (?,?,?,?,?,?,?)")) {

            pst.setString(1, companyName);
            pst.setString(2, Industry);
            pst.setString(3, employeeName);
            pst.setString(4, employeeGender);
            pst.setString(5, Post);
            pst.setString(6, minSalary);
            pst.setString(7, maxSalary);

            pst.executeUpdate();

            JOptionPane.showMessageDialog(this, "Employee data saved successfully!", "Success", JOptionPane.INFORMATION_MESSAGE);

            // Reset fields
            Txtcompany.setText("");
            industry.setSelectedIndex(0);
            Txtemployee.setText("");
            gender.setSelectedIndex(0);
            post.setSelectedIndex(0);
            minsalary.setSelectedIndex(0);
            maxsalary.setSelectedIndex(0);

        } catch (SQLException ex) {
            JOptionPane.showMessageDialog(this, "Database Error: " + ex.getMessage(), "Error", JOptionPane.ERROR_MESSAGE);
        }
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> new Employee().setVisible(true));
    }
}
```

</details>

<br/><hr/><br/>

<details>
  <summary>UoK Form</summary>

  ## Mysql
  ```groovy
  CREATE DATABASE IF NOT EXISTS Uk_form_database;

  USE Uk_form_database;
  
  CREATE TABLE IF NOT EXISTS students (
      student_id    INT          NOT NULL AUTO_INCREMENT,
      full_name     VARCHAR(150) NOT NULL,
      gender        VARCHAR(10)  NOT NULL,
      password      VARCHAR(255) NOT NULL,
      date_of_birth DATE         NOT NULL,
      mobile_number VARCHAR(15)  NOT NULL,
      email_address VARCHAR(150) NOT NULL,
      area          VARCHAR(100) NOT NULL,
      province      VARCHAR(100) NOT NULL,
      nationality   VARCHAR(100) NOT NULL,
      registered_at TIMESTAMP    NOT NULL DEFAULT CURRENT_TIMESTAMP,
      PRIMARY KEY (student_id)
  );
  ```

  ## Script
  ```groovy
  /*
   * Click nbfs://nbhost/SystemFileSystem/Templates/Licenses/license-default.txt to change this license
   * Click nbfs://nbhost/SystemFileSystem/Templates/Classes/Main.java to edit this template
   */
  package netbeansuokform;
  
  /**
   *
   * @author Elysee NIYIBIZI
   * @Reg No: 2305000921
   */
  
  import javax.swing.*;
  import java.awt.*;
  import java.awt.event.*;
  import java.sql.*;
  
  public class NetbeansUoKForm extends JFrame {
  
      private JTextField txtFullName, txtMobile, txtEmail;
      private JPasswordField txtPassword, txtConfirmPassword;
      private JComboBox<String> cmbDay, cmbMonth, cmbYear;
      private JComboBox<String> cmbArea, cmbProvince, cmbNationality;
      private JRadioButton rbMale, rbFemale;
      private ButtonGroup genderGroup;
      private JButton btnSubmit, btnClear;
  
      private static final Color PURPLE_DARK  = new Color(75, 0, 130);
      private static final Color PURPLE_MED   = new Color(102, 51, 153);
      private static final Color PURPLE_LIGHT = new Color(180, 140, 220);
      private static final Color PURPLE_BG    = new Color(245, 235, 255);
  
      private static final String DB_URL  = "jdbc:mysql://localhost:3306/Uk_form_database";
      private static final String DB_USER = "root";
      private static final String DB_PASS = "";
  
      public NetbeansUoKForm() {
          setTitle("University of Kigali - Student Registration");
          setSize(900, 700);
          setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
          setLocationRelativeTo(null);
          setResizable(false);
          buildUI();
          setVisible(true);
      }
  
      private void buildUI() {
          JPanel main = new JPanel(new BorderLayout());
          main.add(buildHeader(),  BorderLayout.NORTH);
          main.add(buildForm(),    BorderLayout.CENTER);
          main.add(buildFooter(), BorderLayout.SOUTH);
          setContentPane(main);
      }
  
      private JPanel buildHeader() {
          JPanel p = new JPanel(new FlowLayout(FlowLayout.LEFT, 18, 12));
          p.setBackground(PURPLE_DARK);
  
          JLabel icon = new JLabel("U");
          icon.setPreferredSize(new Dimension(44, 44));
          icon.setHorizontalAlignment(SwingConstants.CENTER);
          icon.setFont(new Font("Arial", Font.BOLD, 20));
          icon.setForeground(Color.WHITE);
          icon.setOpaque(true);
          icon.setBackground(PURPLE_MED);
  
          JPanel text = new JPanel(new GridLayout(2, 1));
          text.setOpaque(false);
  
          JLabel t1 = new JLabel("UNIVERSITY OF KIGALI");
          t1.setFont(new Font("Arial", Font.BOLD, 20));
          t1.setForeground(Color.WHITE);
  
          JLabel t2 = new JLabel("STUDENT REGISTRATION SYSTEM · MYSQL DATABASE");
          t2.setFont(new Font("Arial", Font.PLAIN, 11));
          t2.setForeground(new Color(200, 180, 230));
  
          text.add(t1);
          text.add(t2);
          p.add(icon);
          p.add(text);
          return p;
      }
  
      private JScrollPane buildForm() {
          JPanel p = new JPanel();
          p.setBackground(Color.WHITE);
          p.setLayout(new BoxLayout(p, BoxLayout.Y_AXIS));
          p.setBorder(BorderFactory.createEmptyBorder(16, 28, 16, 28));
  
          JPanel banner = new JPanel(new GridLayout(2, 1));
          banner.setBackground(PURPLE_DARK);
          banner.setBorder(BorderFactory.createEmptyBorder(10, 14, 10, 14));
          banner.setMaximumSize(new Dimension(Integer.MAX_VALUE, 62));
  
          JLabel b1 = new JLabel("  Student Registration Form");
          b1.setFont(new Font("Arial", Font.BOLD, 15));
          b1.setForeground(Color.WHITE);
  
          JLabel b2 = new JLabel("  Fields marked * are mandatory · Data stored in MySQL");
          b2.setFont(new Font("Arial", Font.PLAIN, 11));
          b2.setForeground(new Color(200, 180, 230));
  
          banner.add(b1);
          banner.add(b2);
          p.add(banner);
          p.add(Box.createVerticalStrut(16));
  
          // Row 1: Full Name | Gender
          JPanel r1 = row();
          txtFullName = field("Enter full name");
          JPanel gp = new JPanel(new FlowLayout(FlowLayout.LEFT, 10, 0));
          gp.setOpaque(false);
          rbMale   = radio("Male");
          rbFemale = radio("Female");
          genderGroup = new ButtonGroup();
          genderGroup.add(rbMale);
          genderGroup.add(rbFemale);
          gp.add(rbMale);
          gp.add(rbFemale);
          r1.add(labeled("Full Name *", txtFullName));
          r1.add(labeled("Gender *", gp));
          p.add(r1);
          p.add(Box.createVerticalStrut(12));
  
          // Row 2: Password | Confirm Password
          JPanel r2 = row();
          txtPassword        = pfield("Min 6 characters");
          txtConfirmPassword = pfield("Re-enter password");
          r2.add(labeled("Password *", txtPassword));
          r2.add(labeled("Confirm Password *", txtConfirmPassword));
          p.add(r2);
          p.add(Box.createVerticalStrut(12));
  
          // Row 3: Date of Birth
          String[] days = new String[32]; days[0] = "DD";
          for (int i = 1; i <= 31; i++) days[i] = String.valueOf(i);
          cmbDay = combo(days);
  
          String[] months = {"Month","January","February","March","April","May","June",
                             "July","August","September","October","November","December"};
          cmbMonth = combo(months);
          cmbMonth.setPreferredSize(new Dimension(200, 36));
  
          String[] years = new String[81]; years[0] = "YYYY";
          for (int i = 1; i <= 80; i++) years[i] = String.valueOf(2024 - i + 1);
          cmbYear = combo(years);
          cmbYear.setPreferredSize(new Dimension(100, 36));
  
          JPanel dob = new JPanel(new FlowLayout(FlowLayout.LEFT, 8, 0));
          dob.setOpaque(false);
          dob.add(cmbDay);
          dob.add(cmbMonth);
          dob.add(cmbYear);
  
          JPanel r3 = new JPanel(new FlowLayout(FlowLayout.LEFT, 0, 0));
          r3.setOpaque(false);
          r3.setMaximumSize(new Dimension(Integer.MAX_VALUE, 72));
          r3.add(labeled("Date of Birth *", dob));
          p.add(r3);
          p.add(Box.createVerticalStrut(12));
  
          // Row 4: Mobile | Email
          JPanel r4 = row();
          txtMobile = field("10-digit e.g. 0788123456");
          txtEmail  = field("e.g. student@uni.ac.rw");
          r4.add(labeled("Mobile Number *", txtMobile));
          r4.add(labeled("E-mail Address *", txtEmail));
          p.add(r4);
          p.add(Box.createVerticalStrut(12));
  
          // Row 5: Area | Province
          JPanel r5 = row();
          cmbArea     = combo(new String[]{"Select area","Nyarugenge","Gasabo","Kicukiro",
                                           "Huye","Musanze","Rubavu","Nyagatare","Muhanga"});
          cmbProvince = combo(new String[]{"Select province","Kigali City","Northern Province",
                                            "Southern Province","Eastern Province","Western Province"});
          r5.add(labeled("Area *", cmbArea));
          r5.add(labeled("State / Province *", cmbProvince));
          p.add(r5);
          p.add(Box.createVerticalStrut(12));
  
          // Row 6: Nationality
          JPanel r6 = row();
          cmbNationality = combo(new String[]{"Select nationality","Rwandan","Ugandan","Kenyan",
                                               "Tanzanian","Burundian","Congolese","Ethiopian","Other"});
          r6.add(labeled("Nationality *", cmbNationality));
          r6.add(new JPanel());
          p.add(r6);
          p.add(Box.createVerticalStrut(20));
  
          // Buttons
          JPanel bp = new JPanel(new FlowLayout(FlowLayout.RIGHT, 10, 0));
          bp.setOpaque(false);
          bp.setMaximumSize(new Dimension(Integer.MAX_VALUE, 46));
          btnClear  = btn("  Clear",  false);
          btnSubmit = btn("  Submit", true);
          btnClear .addActionListener(e -> clearForm());
          btnSubmit.addActionListener(e -> submitForm());
          bp.add(btnClear);
          bp.add(btnSubmit);
          p.add(bp);
  
          return new JScrollPane(p);
      }
  
      private JPanel buildFooter() {
          JPanel p = new JPanel();
          p.setBackground(PURPLE_DARK);
          p.setBorder(BorderFactory.createEmptyBorder(7, 0, 7, 0));
          JLabel l = new JLabel("University of Kigali · Student Registration System · Java Swing + MySQL (JDBC)");
          l.setFont(new Font("Arial", Font.PLAIN, 11));
          l.setForeground(new Color(200, 180, 230));
          p.add(l);
          return p;
      }
  
      private JPanel row() {
          JPanel p = new JPanel(new GridLayout(1, 2, 24, 0));
          p.setOpaque(false);
          p.setMaximumSize(new Dimension(Integer.MAX_VALUE, 72));
          return p;
      }
  
      private JTextField field(String hint) {
          JTextField tf = new JTextField();
          tf.setFont(new Font("Arial", Font.PLAIN, 13));
          tf.setBackground(PURPLE_BG);
          tf.setForeground(new Color(60, 0, 100));
          tf.setBorder(BorderFactory.createCompoundBorder(
              BorderFactory.createLineBorder(PURPLE_LIGHT, 1),
              BorderFactory.createEmptyBorder(5, 8, 5, 8)));
          tf.putClientProperty("JTextField.placeholderText", hint);
          return tf;
      }
  
      private JPasswordField pfield(String hint) {
          JPasswordField pf = new JPasswordField();
          pf.setFont(new Font("Arial", Font.PLAIN, 13));
          pf.setBackground(PURPLE_BG);
          pf.setForeground(new Color(60, 0, 100));
          pf.setBorder(BorderFactory.createCompoundBorder(
              BorderFactory.createLineBorder(PURPLE_LIGHT, 1),
              BorderFactory.createEmptyBorder(5, 8, 5, 8)));
          pf.putClientProperty("JTextField.placeholderText", hint);
          return pf;
      }
  
      private JComboBox<String> combo(String[] items) {
          JComboBox<String> cb = new JComboBox<>(items);
          cb.setFont(new Font("Arial", Font.PLAIN, 13));
          cb.setBackground(PURPLE_BG);
          cb.setForeground(new Color(60, 0, 100));
          cb.setPreferredSize(new Dimension(160, 36));
          return cb;
      }
  
      private JRadioButton radio(String text) {
          JRadioButton rb = new JRadioButton(text);
          rb.setFont(new Font("Arial", Font.PLAIN, 13));
          rb.setForeground(PURPLE_DARK);
          rb.setOpaque(false);
          return rb;
      }
  
      private JButton btn(String text, boolean primary) {
          JButton b = new JButton(text);
          b.setFont(new Font("Arial", Font.BOLD, 13));
          b.setPreferredSize(new Dimension(120, 38));
          b.setCursor(Cursor.getPredefinedCursor(Cursor.HAND_CURSOR));
          b.setFocusPainted(false);
          if (primary) {
              b.setBackground(PURPLE_DARK);
              b.setForeground(Color.WHITE);
              b.setOpaque(true);
              b.setBorder(BorderFactory.createLineBorder(PURPLE_DARK, 2));
          } else {
              b.setBackground(Color.WHITE);
              b.setForeground(PURPLE_DARK);
              b.setOpaque(true);
              b.setBorder(BorderFactory.createLineBorder(PURPLE_DARK, 2));
          }
          return b;
      }
  
      private JPanel labeled(String label, JComponent c) {
          JPanel p = new JPanel(new BorderLayout(0, 4));
          p.setOpaque(false);
          JLabel l = new JLabel(label);
          l.setFont(new Font("Arial", Font.BOLD, 13));
          l.setForeground(PURPLE_DARK);
          p.add(l, BorderLayout.NORTH);
          p.add(c, BorderLayout.CENTER);
          return p;
      }
  
      private void clearForm() {
          txtFullName.setText("");
          txtPassword.setText("");
          txtConfirmPassword.setText("");
          txtMobile.setText("");
          txtEmail.setText("");
          genderGroup.clearSelection();
          cmbDay.setSelectedIndex(0);
          cmbMonth.setSelectedIndex(0);
          cmbYear.setSelectedIndex(0);
          cmbArea.setSelectedIndex(0);
          cmbProvince.setSelectedIndex(0);
          cmbNationality.setSelectedIndex(0);
      }
  
      private void submitForm() {
          String fullName    = txtFullName.getText().trim();
          String password    = new String(txtPassword.getPassword());
          String confirm     = new String(txtConfirmPassword.getPassword());
          String mobile      = txtMobile.getText().trim();
          String email       = txtEmail.getText().trim();
          String gender      = rbMale.isSelected() ? "Male" : rbFemale.isSelected() ? "Female" : "";
          String day         = (String) cmbDay.getSelectedItem();
          String month       = (String) cmbMonth.getSelectedItem();
          String year        = (String) cmbYear.getSelectedItem();
          String area        = (String) cmbArea.getSelectedItem();
          String province    = (String) cmbProvince.getSelectedItem();
          String nationality = (String) cmbNationality.getSelectedItem();
  
          if (fullName.isEmpty())                           { err("Full Name is required.");             return; }
          if (gender.isEmpty())                             { err("Please select a gender.");            return; }
          if (password.length() < 6)                        { err("Password must be at least 6 chars."); return; }
          if (!password.equals(confirm))                    { err("Passwords do not match.");            return; }
          if (day.equals("DD")||month.equals("Month")||year.equals("YYYY"))
                                                            { err("Please complete Date of Birth.");     return; }
          if (!mobile.matches("\\d{10}"))                   { err("Mobile must be 10 digits.");          return; }
          if (!email.contains("@") || !email.contains(".")) { err("Enter a valid email address.");       return; }
          if (area.equals("Select area"))                   { err("Please select an area.");             return; }
          if (province.equals("Select province"))           { err("Please select a province.");          return; }
          if (nationality.equals("Select nationality"))     { err("Please select a nationality.");       return; }
  
          String dob = year + "-"
                     + String.format("%02d", cmbMonth.getSelectedIndex()) + "-"
                     + String.format("%02d", Integer.parseInt(day));
  
          String sql = "INSERT INTO students "
                     + "(full_name, gender, password, date_of_birth, mobile_number, "
                     + " email_address, area, province, nationality) "
                     + "VALUES (?, ?, ?, ?, ?, ?, ?, ?, ?)";
  
          try (Connection con = DriverManager.getConnection(DB_URL, DB_USER, DB_PASS);
               PreparedStatement ps = con.prepareStatement(sql)) {
  
              ps.setString(1, fullName);
              ps.setString(2, gender);
              ps.setString(3, password);
              ps.setString(4, dob);
              ps.setString(5, mobile);
              ps.setString(6, email);
              ps.setString(7, area);
              ps.setString(8, province);
              ps.setString(9, nationality);
  
              ps.executeUpdate();
  
              JOptionPane.showMessageDialog(this,
                  "Student registered successfully!\nWelcome, " + fullName + "!",
                  "Success", JOptionPane.INFORMATION_MESSAGE);
              clearForm();
  
          } catch (SQLException ex) {
              err("Database error:\n" + ex.getMessage());
              ex.printStackTrace();
          }
      }
  
      private void err(String msg) {
          JOptionPane.showMessageDialog(this, msg, "Error", JOptionPane.ERROR_MESSAGE);
      }
  
      public static void main(String[] args) {
          try {
              Class.forName("com.mysql.cj.jdbc.Driver");
          } catch (ClassNotFoundException e) {
              JOptionPane.showMessageDialog(null,
                  "MySQL JDBC Driver not found!\nAdd mysql-connector-j.jar to your classpath.",
                  "Driver Error", JOptionPane.ERROR_MESSAGE);
              return;
          }
          SwingUtilities.invokeLater(NetbeansUoKForm::new);
      }
  }
  ```
</details>

<br/><hr/><br/>

<details>
  <summary>Calculator</summary>

  ## Solve btn
  ```groovy
  private void jButton1ActionPerformed(java.awt.event.ActionEvent evt) {                                         
        // TODO add your handling code here:
        try {
            double num1 = Double.parseDouble(TxtNum1.getText()); 
            double num2 = Double.parseDouble(TxtNum2.getText());

            double res;

            if (addRadio.isSelected()) {
                res = num1 + num2;
            } else if (subRadio.isSelected()) {
                res = num1 - num2;
            } else if (mulRadio.isSelected()) {
                res = num1 * num2;
            } else if (divRadio.isSelected()) {
                if (num2 == 0) {
                    resLabel.setText("Cannot divide by zero!");
                    return;
                }
                res = num1 / num2;
            } else {
                resLabel.setText("Please select an operation!");
                return;
            }

            resLabel.setText(String.format("The answer is: %.2f", res));
        } catch (NumberFormatException e) {
            resLabel.setText("Invalid input! Please enter valid numbers.");
        }
    }
  ```

  ## Exit
  ```groovy
  System.exit(0);
  ```
</details>

<br/><hr/><br/>

<details>
  <summary>DB Connection</summary>

  ## Script btn
  ```groovy
  String code = text1.getText();
  String name = text2.getText();
  try {
      Class.forName("com.mysql.cj.jdbc.Driver");
      
      String url = "jdbc:mysql://localhost:3306/school";
      String username = "root";
      String password = "";
      
      Connection conn = DriverManager.getConnection(url, username, password);
      System.out.println("CONNECTED SUCCESSFULLY");
      
      // Insert Records!!!
      Statement stm = conn.createStatement();
      
      String sql = "INSERT INTO student (code, name) VALUES ('" + code + "', '" + name + "')";
      stm.executeUpdate(sql);
      JOptionPane.showMessageDialog(this, "ADDED SUCCESSFULLY\n" + sql);
      
  } catch(Exception e) {
      System.out.println("ERROR, NOT CONNECTED: " + e.getMessage());
  }
  ```
</details>

<br/><hr/><br/>

<details>
  <summary>JavaBeans</summary>

  # JavaBeans
  Write a Java class named Student that follows JavaBeans conventions. The class should include a 
  private property called name to store the student’s name. It should provide a no-argument 
  constructor, along with methods that allow setting and retrieving the value of the name property. 
  The class must also support object serialization so that its objects can be saved to a file.

  ```groovy
  /*
 * Click nbfs://nbhost/SystemFileSystem/Templates/Licenses/license-default.txt to change this license
 * Click nbfs://nbhost/SystemFileSystem/Templates/Classes/Class.java to edit this template
 */
package JavaBeans;

import java.io.Serializable;

/**
 *
 * @author Elysee NIYIBIZI
 */

public class Student implements Serializable {

    // Private property
    private String name;

    // No-argument constructor
    public Student() {
    }

    // Getter method
    public String getName() {
        return name;
    }

    // Setter method
    public void setName(String name) {
        this.name = name;
    }
}
```

---

By adding a main application class named MainApp that demonstrates how a Student object can 
be saved to a file and later loaded back into the program. The program should first create a Student 
object and assign a name to it. It should then save the object into a file using object serialization. 
After saving the object, the program should read the same object back from the file using 
deserialization and display the student’s name on the screen. During execution, the program must 
print confirmation messages. When the object is successfully saved, it should display "Object has 
been serialized (saved)." When the object is successfully loaded, it should display "Object has been 
deserialized (loaded)." Finally, it should display the student’s name in the format "Student Name: 
Mugabo Mohammed".

```groovy
/*
 * Click nbfs://nbhost/SystemFileSystem/Templates/Licenses/license-default.txt to change this license
 * Click nbfs://nbhost/SystemFileSystem/Templates/Classes/Class.java to edit this template
 */
package JavaBeans;

import java.io.FileOutputStream;
import java.io.FileInputStream;
import java.io.ObjectOutputStream;
import java.io.ObjectInputStream;
import java.io.IOException;

/**
 *
 * @author Elysee NIYIBIZI
 */

public class MainApp {

    public static void main(String[] args) {

        // Create object
        Student student = new Student();
        student.setName("Mugabo Mohammed");

        // File name
        String filename = "student.ser";

        // -------- SERIALIZATION (Saving) --------
        try {
            FileOutputStream fileOut = new FileOutputStream(filename);
            ObjectOutputStream out = new ObjectOutputStream(fileOut);

            out.writeObject(student);
            out.close();
            fileOut.close();

            System.out.println("Object has been serialized (saved).");

        } catch (IOException e) {
            e.printStackTrace();
        }

        // -------- DESERIALIZATION (Loading) --------
        try {
            FileInputStream fileIn = new FileInputStream(filename);
            ObjectInputStream in = new ObjectInputStream(fileIn);

            Student loadedStudent = (Student) in.readObject();

            in.close();
            fileIn.close();

            System.out.println("Object has been deserialized (loaded).");
            System.out.println("Student Name: " + loadedStudent.getName());

        } catch (IOException | ClassNotFoundException e) {
            e.printStackTrace();
        }
    }
}
```
</details>




