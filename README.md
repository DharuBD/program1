print_spaces() {
  for ((j=0; j<$1; j++)); do
    echo -n " "
  done
}
while true; do
  echo -n "Enter n (positive integer): "
  read rows
  if [[ "$rows" =~ ^[0-9]+$ ]] && [ "$rows" -gt 0 ]; then
    break
  else
    echo "Invalid input. Please enter a positive integer."
  fi
done
max_num=$(( (1 << rows) / 2 ))  # Largest number in the last row
alignment_width=${#max_num}
for ((i=0; i<rows; i++)); do
  # Print leading spaces for alignment
  print_spaces $((rows - i))
  num=1
  for ((k=0; k<=i; k++)); do
    # Print the current number with specified alignment
    printf "%${alignment_width}d " "$num"
    num=$((num * (i - k) / (k + 1)))
  done
  echo
done
