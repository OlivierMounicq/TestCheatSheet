## 1/ Get node quantity

```cs
namespace TreeModel
{
    internal class Program
    {
        static void Main(string[] args)
        {
            var tree = new Node<int>
            {
                Value = 1,
                Children = new List<Node<int>> 
                {
                    new Node<int>
                    {
                        Value = 2,
                        Children = new List<Node<int>> 
                        { 
                            new Node<int>{ Value = 3},
                            new Node<int>{ Value = 4},
                            new Node<int>{ Value = 5},
                        }
                    },
                    new Node<int>{ Value = 6},
                }
            };

            var nodeQty = TreeExtension.NodeQuantity(tree) + 1;
        }
    }

    public static class TreeExtension
    {
        public static int NodeQuantity<T>(Node<T> node)
        {
            var currentQty = node.Children?.Count() ?? 0;

            if(node.Children != null && node.Children.Any()) 
            { 
                foreach(var child in node.Children)
                {
                    currentQty += NodeQuantity(child);
                }
            }

            return currentQty;
        }
    }

    public class Node<T>
    {
        public T Value { get; set; }
        public IEnumerable<Node<T>> Children { get; set;}
    }
}
```
