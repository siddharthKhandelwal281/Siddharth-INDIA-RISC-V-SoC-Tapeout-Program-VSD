#  Day 5: IF/CASE Constructs, Latch Inference & Generate Statements

This session focused on how **control structures** in Verilog (IF/CASE) affect synthesis, how to avoid **unintended latches**, and how **generate constructs** simplify structural design.

---

## 1️⃣ IF/CASE Constructs

* **Purpose:** Used for conditional logic, typically synthesizing to multiplexers.
* **Rule:** A complete IF/CASE must assign outputs on all possible paths → prevents **latch inference**.

### Key Cases:

* **Incomplete IF** → missing `else` causes latch inference.
* **Overlapping CASE** → multiple matches → ambiguity. Use `unique case` or ordered if-else.
* **Default branch** → always provide default to cover all possibilities.

---

## 2️⃣ Latch Inference

* Happens when outputs are **not assigned** in some paths of a combinational always block.
* Synthesis inserts **level-sensitive latches** to hold values.
* Latches → bad for timing, cause sim-synth mismatches.
* **Best Practice:** Always assign outputs in all branches (`else` or `default`).

---

## 3️⃣ For Loop in RTL

* Synthesizable when loop bounds are **static constants**.
* Expands into replicated hardware logic, not runtime iteration.
* Used as coding convenience (e.g., MUX, DEMUX, RCA).

---

## 🧪 Lab Tasks & Code Examples

### 🔹 Incomplete vs Complete Constructs

```verilog
// Incomplete Case → may infer latch
module incomp_case (input i0, input i1, input i2, input [1:0] sel, output reg y);
 always @(*) begin
   case (sel)
     2'b00: y = i0;
     2'b01: y = i1;
   endcase
 end
endmodule
```
<img width="1856" height="1046" alt="image" src="https://github.com/user-attachments/assets/2acbec8b-a142-4d53-8e5d-9e2cedb0606a" />
<img width="1856" height="1046" alt="image" src="https://github.com/user-attachments/assets/593482e6-a26e-4f9d-ba87-8a97c2fad127" />


```verilog
// Complete Case → safe
module comp_case (input i0, input i1, input i2, input [1:0] sel, output reg y);
 always @(*) begin
   case (sel)
     2'b00: y = i0;
     2'b01: y = i1;
     default: y = i2;
   endcase
 end
endmodule
```

<img width="1856" height="1046" alt="image" src="https://github.com/user-attachments/assets/c731f6a1-58ce-4ced-84d8-7f1440b224a7" />

<img width="1856" height="1046" alt="image" src="https://github.com/user-attachments/assets/31d9834c-78c3-4676-bec9-6bd3d260d377" />


```verilog
// Incomplete IF
module incomp_if (input i0, input i1, input i2, output reg y);
 always @(*) begin
   if (i0)
     y <= i1;
   // Missing else → latch inferred
 end
endmodule
```

<img width="1856" height="1046" alt="image" src="https://github.com/user-attachments/assets/29b86bfc-e1e8-4d0a-b1fb-7f67edc7e265" />
<img width="1856" height="1046" alt="image" src="https://github.com/user-attachments/assets/ef54b323-c020-41c6-9caf-4372c684ddd3" />


```verilog
// Incomplete Nested IF
module incomp_if2 (input i0, input i1, input i2, input i3, output reg y);
 always @(*) begin
   if (i0)
     y <= i1;
   else if (i2)
     y <= i3;
   // Missing final else → latch inferred
 end
endmodule
```
<img width="1856" height="1046" alt="image" src="https://github.com/user-attachments/assets/1dd62805-58c5-4a90-bef0-9010d91f263a" />
<img width="1856" height="1046" alt="image" src="https://github.com/user-attachments/assets/f4f593cf-cbb4-4aea-b1af-6f0977cf016f" />

---

### 🔹 Bad Case Example

```verilog
module bad_case (input i0, input i1, input i2, input i3, input [1:0] sel, output reg y);
 always @(*) begin
   case (sel)
     2'b00: y = i0;
     2'b01: y = i1;
     2'b10: y = i2;
     // Missing sel=2'b11 → latch inferred
   endcase
 end
endmodule
```
<img width="1856" height="1046" alt="image" src="https://github.com/user-attachments/assets/1392205e-757d-42bc-a7b7-fc30fbdff454" />
<img width="1856" height="1046" alt="image" src="https://github.com/user-attachments/assets/8a58304a-4fbc-429c-af0f-76282d8001b3" />

---

### 🔹 Generate with For Loops

**MUX (using generate loop):**

```verilog
module mux_generate (input i0, input i1, input i2, input i3,
                     input [1:0] sel, output reg y);
  wire [3:0] i_int = {i3, i2, i1, i0};
  integer k;
  always @(*) begin
    for (k = 0; k < 4; k = k + 1)
      if (k == sel)
        y = i_int[k];
  end
endmodule
```
<img width="1856" height="1046" alt="image" src="https://github.com/user-attachments/assets/bc58878c-9f81-4977-bff8-e71843cf50ff" />
<img width="1856" height="1046" alt="image" src="https://github.com/user-attachments/assets/7337096c-0ed7-47b4-8371-1048afbc0d49" />

```verilog
// demux_case.v
module demux_case (output o0, output o1, output o2, output o3, output o4, output o5, output o6, output o7,
                   input [2:0] sel, input i);
  reg [7:0] y_int;
  assign {o7, o6, o5, o4, o3, o2, o1, o0} = y_int;
  integer k;
  always @(*)
  begin
    y_int = 8'b0;
    case (sel)
      3'b000: y_int[0] = i;
      3'b001: y_int[1] = i;
      3'b010: y_int[2] = i;
      3'b011: y_int[3] = i;
      3'b100: y_int[4] = i;
      3'b101: y_int[5] = i;
      3'b110: y_int[6] = i;
      3'b111: y_int[7] = i;
    endcase
  end
endmodule
```
<img width="1856" height="1046" alt="image" src="https://github.com/user-attachments/assets/f1fa5f65-e3c5-4118-9243-a9fad181a5fc" />
```verilog

// demux_generate.v
module demux_generate (output o0, output o1, output o2, output o3, output o4, output o5, output o6, output o7,
                       input [2:0] sel, input i);
  reg [7:0] y_int;
  assign {o7, o6, o5, o4, o3, o2, o1, o0} = y_int;
  integer k;
  always @(*)
  begin
    y_int = 8'b0;
    for (k = 0; k < 8; k = k + 1) begin
      if (k == sel)
        y_int[k] = i;
    end
  end
endmodule
```
<img width="1856" height="1046" alt="image" src="https://github.com/user-attachments/assets/b4e77d53-0cb3-4609-b3cb-bbcfcbad85a8" />

### 🔹 Ripple Carry Adder (RCA) with Generate

```verilog
module rca (input  [7:0] num1, input [7:0] num2, output [8:0] sum);
  wire [7:0] int_sum, int_co;

  genvar i;
  generate
    for (i = 1; i < 8; i = i + 1) begin
      fa u_fa (.a(num1[i]), .b(num2[i]), .c(int_co[i-1]),
               .co(int_co[i]), .sum(int_sum[i]));
    end
  endgenerate

  fa u_fa0 (.a(num1[0]), .b(num2[0]), .c(1'b0), .co(int_co[0]), .sum(int_sum[0]));

  assign sum[7:0] = int_sum;
  assign sum[8]   = int_co[7];
endmodule

module fa (input a, input b, input c, output co, output sum);
  assign {co, sum} = a + b + c;
endmodule
```
<img width="1856" height="1046" alt="image" src="https://github.com/user-attachments/assets/db6ec284-ecd6-4439-b9cd-b1ce3c1a76a5" />


---

## 💡 Analysis & Takeaways

* ✅ Always **cover all paths** in IF/CASE → prevents unintended latches.
* ✅ Use **default branches** in case statements.
* ✅ Use **for-generate** loops for structural replication (MUX, DEMUX, Adders).
* ✅ Avoid unintended latches → design will be synthesis-friendly and match simulation.

---
