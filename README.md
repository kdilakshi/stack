# stack
implementation(push)
import java.util.LinkedList;
import java.util.Queue;

class StackUsingTwoQueues {
    Queue<Integer> queue1 = new LinkedList<>();
    Queue<Integer> queue2 = new LinkedList<>();

    // Push element onto stack
    public void push(int x) {
        queue1.add(x);
    }

    // Removes the element on top of the stack
    public int pop() {
        if (queue1.isEmpty()) {
            System.out.println("Stack is empty");
            return -1;
        }

        // Move elements from queue1 to queue2, except the last one
        while (queue1.size() > 1) {
            queue2.add(queue1.remove());
        }

        // Last element in queue1 is the top of the stack
        int poppedElement = queue1.remove();

        // Swap queue1 and queue2
        Queue<Integer> temp = queue1;
        queue1 = queue2;
        queue2 = temp;

        return poppedElement;
    }

    // Get the top element
    public int top() {
        if (queue1.isEmpty()) {
            System.out.println("Stack is empty");
            return -1;
        }

        while (queue1.size() > 1) {
            queue2.add(queue1.remove());
        }

        int topElement = queue1.peek(); // Peek at last element
        queue2.add(queue1.remove()); // Move last element to queue2

        // Swap queues
        Queue<Integer> temp = queue1;
        queue1 = queue2;
        queue2 = temp;

        return topElement;
    }

    // Check if stack is empty
    public boolean isEmpty() {
        return queue1.isEmpty();
    }

    public static void main(String[] args) {
        StackUsingTwoQueues stack = new StackUsingTwoQueues();
        stack.push(10);
        stack.push(20);
        stack.push(30);

        System.out.println("Top element: " + stack.top()); // Output: 30
        System.out.println("Popped element: " + stack.pop()); // Output: 30
        System.out.println("Top element: " + stack.top()); // Output: 20
    }
}
