bsearch
  searches for target in middle of array each iteration
  assume sorted input
  return idx of target

def bsearch(arr, target)
  return nil if arr.empty?

  left = arr[0...middle_idx]
  right = arr[middle_idx..-1]
  middle_idx = arr.length / 2

  case self[middle_idx] <=> target
  when 1
    bsearch(left, target)
  when 0
    middle_idx
  when -1
    idx = bsearch(right, target)
    idx ? idx + middle_idx : nil
  end
end

my each 
patch into Array
call a pass block of each ele of the array

class Array
  def my_each(&prc)
    idx = 0
    while idx < length
      prc.call(self[idx])
      idx += 1
    end
    self
  end
end

arr method
dups 
hash dup = [indicies]

class Array
  def dups
    dup_hash = Hash.new { |hash, k| hash[k] = [] }
    
    each_with_index |ele, idx|
      dup_hash[ele] << idx
    end

    dup_hash.select { |letter, indicies| indicies.length > 1 }
  end
end

#recursively find the first n factorials
#n(0) == 1
#n(1) == n * n(0)
#n(2) == n * n(1) 
#n(3) == n * n(2)
#(n(0)!..n!(num - 1))

def factorials(n)
  return [1] if n == 0
  prev_facts = factorials(n - 1)
  prev_facts + [n * prev_facts[-1]]
end