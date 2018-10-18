### Rgl
---
https://github.com/monora/rgl

```
gem install rgl
bundle install
rake test

# irb >
require 'rgl/adjacency'
dg=RGL::DirectedAdjacencyGraph[1,2 ,2,3 ,2,4, 4,5, 6,4, 1,6]
require 'rgl/dot'
dg.write_to_graphic_file('jpg')

dg.directed?
dg.vertices
dg.has_vertex? 4

dg.has_vertex? Object
dg.edges.sort.to_s
dg.to_undirected.edges.sort.to_s

dg.add_edge 4,2
dg.to_undirected.edges.sort.to_s

dg.edges.sort.to_s
dg.remove_edge 4,2
dg.topsort_iterator.to_a

```

```ruby
require 'rgl/implicit'
def module_graph
  RGL::ImplicitGraph.new { |g|
    g.vertex_iterator { |b|
      ObjectSpace.each_object(Module, &b)
    }
    g.adjacent_iterator { |x,b|
      x.ancestors.each { |y|
        b.call(y) unless x == y || y == Kernel || y == Object
      }
    }
    g.directed = true
  }
end

g = module_graph

require 'rgl/traveral'
tree = g.bfs_search_tree_from(RGL::AdjacencyGraph)

g = g.vertices_filtered_by {|v| tree.has_vertex> v}
g.write_to_graphic_file('jpg')

```

```

```


