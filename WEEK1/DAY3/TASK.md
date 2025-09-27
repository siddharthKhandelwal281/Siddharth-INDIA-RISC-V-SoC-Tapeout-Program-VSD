# 📘 Day 3: Combinational and Sequential Optimizations

This session covers optimization techniques in RTL design to reduce **area**, **power**, and improve **timing closure**.

---

## 🔹 Topics Covered

* **Combinational logic optimization**

  * Reduce gates via constant propagation & Boolean simplification.

* **Sequential logic optimization**

  * Optimize registers with constant propagation.
  * Advanced techniques: **state optimization**, **retiming**, **logic cloning**.

---

## 🔹 Constant Propagation

When signals are tied to `0` or `1`, logic simplifies.

**Example:**

```
Y = ((A & B) | C)'   →   Y = C'   (when A = 0)
```

✅ **Benefit:** fewer transistors → lower dynamic power due to less toggling.

---

## 🔹 Sequential Constant Propagation

When a register output is **always constant**, the downstream logic can be collapsed.

**Example:**

* If `Q = 0` after reset and it drives an AND gate → output always `0` → path removed.

---

## 🔹 Boolean Logic Optimization

Combines **algebraic reduction** + **mux-level reasoning** to simplify RTL.

**Example:**

* A nested ternary reduces to:

```
Y = A ⊕ C
```

👉 Eliminates redundant gates and product terms.

---

## 🔹 Why Optimization Matters

* ⚡ **Reduced gate count** → lower silicon area & power.
* 📉 **Less toggle activity** → reduced dynamic power.
* ⏱️ **Improved timing closure** → shorter critical paths.

---

## 💻 Example Verilog Snippets

### 📂 opt_check.v

```verilog
module opt_check (input a, input b, output y);
  assign y = a ? b : 0;
endmodule
```
<img width="572" height="181" alt="image" src="https://github.com/user-attachments/assets/b4aec7d6-7e81-406a-acab-48c47ba87fee" />
<img width="1856" height="1042" alt="image" src="https://github.com/user-attachments/assets/5aadced4-aff6-4dfe-91b4-32a59c3608b9" />
<img width="755" height="275" alt="image" src="https://github.com/user-attachments/assets/19688ded-a966-431c-9149-6063dfd8de08" />

### 📂 opt_check2.v

```verilog
module opt_check2 (input a, input b, output y);
  assign y = a ? 1 : b;
endmodule
```
<img width="603" height="150" alt="image" src="https://github.com/user-attachments/assets/a2ec7a2a-9c83-4ec3-884e-f17741e32bbc" />
<img width="1858" height="1049" alt="image" src="https://github.com/user-attachments/assets/4b328170-746a-4e17-9d6e-44f73e1cbf5d" />
<img width="834" height="277" alt="image" src="https://github.com/user-attachments/assets/de4fe5ea-4bea-4cbb-8a45-66cc0390a374" />

### 📂 opt_check3.v

```verilog
module opt_check3 (input a, input b, input c, output y);
  assign y = a ? (c ? b : 0) : 0;
endmodule
```
<img width="608" height="307" alt="image" src="https://github.com/user-attachments/assets/134cdf3e-0712-49ae-abd9-2810867dafde" />
<img width="1858" height="1045" alt="image" src="https://github.com/user-attachments/assets/43859ea6-61a4-48f4-b3cb-78a7f0b3ec1e" />
<img width="771" height="326" alt="image" src="https://github.com/user-attachments/assets/7a6b8d51-fd63-4e89-a465-6382430aa3ae" />

---

### 📂 dff_const1.v

```verilog
module dff_const1 (input clk, input reset, output reg q);
  always @(posedge clk, posedge reset) begin
    if (reset)
      q <= 1'b0;
    else
      q <= 1'b1;
  end
endmodule
```
<img width="679" height="454" alt="image" src="https://github.com/user-attachments/assets/e4c70d81-f152-450d-b3a9-2b35e02b2754" />
<img width="1853" height="1039" alt="image" src="https://github.com/user-attachments/assets/6d76c64e-2398-4f26-911a-928cb9198a1f" />
<img width="675" height="315" alt="image" src="https://github.com/user-attachments/assets/5018357b-ddca-4afc-bd76-b51bfb2bb0d0" />

### 📂 dff_const2.v

```verilog
module dff_const2 (input clk, input reset, output reg q);
  always @(posedge clk, posedge reset) begin
    if (reset)
      q <= 1'b1;
    else
      q <= 1'b1;
  end
endmodule
```
<img width="1853" height="1039" alt="image" src="https://github.com/user-attachments/assets/12887e36-8b00-4b33-91bd-4d050d36e971" />
<img width="448" height="448" alt="image" src="https://github.com/user-attachments/assets/d868b84a-36e8-41f3-938f-529b44728dde" />

### 📂 dff_const3.v

```verilog
module dff_const3 (input clk, input reset, output reg q);
  reg q1;
  always @(posedge clk, posedge reset) begin
    if (reset) begin
      q  <= 1'b1;
      q1 <= 1'b0;
    end else begin
      q1 <= 1'b1;
      q  <= q1;
    end
  end
endmodule
```
<img width="782" height="469" alt="image" src="https://github.com/user-attachments/assets/4e25a7c1-8e5e-4252-b858-1a9315281ea4" />
<img width="1853" height="1039" alt="image" src="https://github.com/user-attachments/assets/a52d8ecd-08be-42e7-8c3b-9516af73236a" />
<img width="1259" height="479" alt="image" src="https://github.com/user-attachments/assets/ed3a2fa8-64ac-4d93-b9a3-c9a4e58d2c68" />

---

### 📂 counter_opt.v

```verilog
module counter_opt (input clk, input reset, output q);
  reg [2:0] count;
  assign q = count[0];

  always @(posedge clk, posedge reset) begin
    if (reset)
      count <= 3'b000;
    else
      count <= count + 1;
  end
endmodule
```
<img width="1769" height="483" alt="image" src="https://github.com/user-attachments/assets/f1b15b7e-141d-4dad-96da-6fab67405401" />

---

## ✅ Takeaways

* Always check for **constants** in design → collapse unnecessary logic.
* Optimize **sequential logic** by removing unused or constant-driven registers.
* Boolean simplification directly saves **area** & improves **power efficiency**.
