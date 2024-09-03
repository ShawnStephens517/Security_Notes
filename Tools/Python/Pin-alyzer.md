```python
def generate_four_digit_numbers():
    numbers = [f"{i:04}" for i in range(10000)]
    return numbers

def write_numbers_to_file(numbers, filename="four_digit_numbers.txt"):
    with open(filename, "w") as file:
        for number in numbers:
            file.write(number + "\n")

if __name__ == "__main__":
    numbers = generate_four_digit_numbers()
    write_numbers_to_file(numbers)
    print(f"Successfully wrote {len(numbers)} numbers to 'four_digit_numbers.txt'.")

```