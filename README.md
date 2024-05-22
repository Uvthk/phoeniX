Computer Organization - Spring 2024
==============================================================
## Iran Univeristy of Science and Technology
## Assignment 1: Assembly code execution on phoeniX RISC-V core

- Name: mohammad erfan mahtabi
- Team Members: fatemeh ackbari & seyed mohammad reza hedayati
- Student ID: 99413154
- Date: 2024/05/22

## Report

### Quicksort in RISC-V Assembly

#### Overview
This RISC-V assembly program implements the quicksort algorithm to sort an array of integers. The quicksort algorithm is a highly efficient sorting algorithm and works by partitioning an array into two halves, then recursively sorting each half.

#### Program Structure
The program is organized into the following main sections:
1. **Initialization**: Setting up the stack pointer, loading initial values, and preparing the array to be sorted.
2. **Main Execution**: Calling the `QUICKSORT` function and then exiting the program.
3. **Quicksort Function**: The implementation of the quicksort algorithm.
4. **Partition Function**: A helper function used by quicksort to partition the array.
5. **Exit**: Loading the sorted array into registers and halting the program.

#### Detailed Explanation

1. **Initialization**:
    - The stack pointer is adjusted to create space for the program's needs.
    - Registers `a0` to `a5` are initialized with values. Specifically, an array is loaded into memory at address `a0`, with values `[5, 4, 3, 2, 1]`.
    - The start (`a1`) and end (`a2`) indices of the array are set to `0` and `4`, respectively.

    ```assembly
    addi sp, sp, 1000
    li a0, 0
    li s10, -1
    li s11, 5
    ...
    li a1, 0 # start
    li a2, 4 # end
    ```

2. **Main Execution**:
    - The `QUICKSORT` function is called to sort the array.
    - The program then jumps to the `EXIT` label to terminate.

    ```assembly
    jal ra, QUICKSORT
    jal ra, EXIT
    ```

3. **Quicksort Function**:
    - The function starts by saving registers and initializing local variables.
    - The base case for recursion is checked: if the start index is greater than or equal to the end index, the function returns.
    - The `PARTITION` function is called to partition the array.
    - The `QUICKSORT` function is recursively called on the left and right sub-arrays.

    ```assembly
    QUICKSORT:
    addi sp, sp, -20
    ...
    jal ra, PARTITION
    ...
    jal ra, QUICKSORT  # quicksort(arr, start, pi - 1);
    ...
    jal ra, QUICKSORT  # quicksort(arr, pi + 1, end);
    ```

4. **Partition Function**:
    - This function partitions the array around a pivot element.
    - It places elements smaller than the pivot to its left and larger elements to its right.
    - The function uses a loop to swap elements as needed to maintain the partitioning.

    ```assembly
    PARTITION:
    addi sp, sp, -4
    ...
    lw t0, 0(t0)     # pivot = arr[end]
    ...
    LOOP:
    BEQ t2, a2, LOOP_DONE   # while (j < end)
    ...
    SWAP:
    ...
    ```

5. **Exit**:
    - The sorted array is loaded into registers `x21` to `x25`.
    - The program halts with an `ebreak` instruction.

    ```assembly
    EXIT:
    lw x21,0(a0)
    lw x22,4(a0)
    lw x23,8(a0)
    lw x24,12(a0)
    lw x25,16(a0)
    ebreak
    ```

- Attach the waveform image to the README.md file