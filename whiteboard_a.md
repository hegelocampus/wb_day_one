merge sort, takes proc, no mutation

def merge_sort(&prc)
    prc ||= Proc.new { |left, right| left <=> right }
    return self.dup if self.length <= 1

    middle = self.length / 2
    left = self[0...middle]
    right = self[middle..-1]

    left_sort = left.merge_sort(&prc)
    right_sorted = right.merge_sort(&prc)

    Array.merge(left, right, &prc)
end

def self.merge(left, right, &prc)
    sorted = []

    until left.empty? || right.empty?
        if prc.call(left[0], right[0]) == -1
            sorted << left.shift
        else
            sorted << right.shift
        end
    end
    sorted + left + right
end


monkey patch my_flatten
flattens array to specified level
if no level given then flattens to 1d

class Array
    def my_flatten(n = nil)
        return self.dup if n == 0
        n -= 1 unless n.nil?
        flattened = []
        self.each do |ele|
            if ele.is_a?(Array)
                flattened += ele.my_flatten(n)
            else
                flattened << ele.dup
            end
        end
        flattened
    end
end


my_reduce
array method calls block on each element

class Array

    def my_reduce(accumulator = nil, &prc)
        #prc ||= Proc.new { |accumulator, ele| accumulator + ele }
        start = 1 if accumulator.nil?
        start ||= 0
        accumulator ||= self[0]

        self[start..-1].each do |ele|
            accumulator = prc.call(accumulator, ele)
        end
        accumulator
    end

end


shuffled sentence detector
(return true if words can be shuffled into given sentence

def shuffled_sentence_detector(sentence, target)
    sentence.split.sort == target.split.sort
end


n fibs recursively

def fib_list(length)
    return [0, 1].take(length) if length <= 2
    previous_fibs = fib_list(n - 1)
    next_fib = [previous_fibs[-1] + previous_fibs[-2]]
    previous_fibs + next_fib
end

