<table>
  <thead>
    <tr>
      <th>System name</th>
      <th>Status</th>
      <th>Category</th>
      <th>Focus</th>
      <th>Focus area</th>
      <th>Grouping</th>
      <th>Funders</th>
      <th>Nodes</th>
      <th>Accelerators</th>
      <th>Accelerator count per node</th>
      <th>Manufacturer</th>
      <th>Scheduler</th>
      <th>Interconnects</th>
      <th>Reference</th>
    </tr>
  </thead>
  <tbody>
    {% for system in site.systems %}
    <tr>
      <td><a href="{{ system.url }}">{{ system.name }}</a></td>
      <td>{{ site.data.statuses[system.status]["shortdescription"] }}</td>
      <td>{{ site.data.categories[system.category]["shortdescription"] }}</td>
      <td>{{ site.data.focuses[system.focus]["shortdescription"] }}</td>
      <td>{{ system.focus-detail }}</td>
      <td>{{ system.grouping }}</td>
      <td>{{ system.funders | join: "<br>" }}</td>
      <td>{{ system.nodes }}</td>
      <td>{{ system.accelerators | join: "<br>" }}</td>
      <td>{{ system.accelerator-count }}</td>
      <td>{{ system.manufacturer }}</td>
      <td>{{ system.scheduler }}</td>
      <td>{{ system.interconnects | join: "<br>" }}</td>
      <td><a href="{{ system.reference }}">Link</a></td>
    </tr>
    {% endfor %}
  </tbody>
</table>
