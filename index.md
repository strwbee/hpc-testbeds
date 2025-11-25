---
page_css:
- "https://cdn.datatables.net/2.3.5/css/dataTables.dataTables.min.css"
---


<script src="https://code.jquery.com/jquery-3.7.1.js" crossorigin=""></script>
<script src="https://cdn.datatables.net/2.3.5/js/dataTables.min.js" crossorigin=""></script>

## SHAREing HPC Testbeds

The table below shows
a list of HPC testbed and production systems available to UK researchers.
For each system,
click its name to find out more about that system.

<table id="systems" class="display">
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
      {% if system.url == "/systems/system-template/" %}
        {% continue %}
      {% endif %}
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
  <tfoot> <!-- add empty space to indicate we want to have a filter drop-down -->
    <th></th>
    <th>&nbsp;</th> <!-- Status -->
    <th>&nbsp;</th> <!-- Categories -->
    <th>&nbsp;</th> <!-- Focus -->
    <th>&nbsp;</th> <!-- Focus detail -->
    <th>&nbsp;</th> <!-- Grouping -->
    <th></th>
    <th></th>
    <th></th>
    <th></th>
    <th>&nbsp;</th> <!-- Manufacturer -->
    <th>&nbsp;</th> <!-- Scheduler -->
    <th></th>
    <th></th>
  </tfoot>
</table>

<script>
let table = new DataTable(
  '#systems',
  {
    scrollX: true,
    initComplete: function () {
        this.api()
            .columns()
            .every(function () {
                let column = this;

                if (column.footer().innerHTML == '<div class="dt-column-footer"><span class="dt-column-title"></span></div>') {
                  return;
                }

                // Create select element
                let select = document.createElement('select');
                select.style.width = "100%";
                select.add(new Option(''));
                column.footer().replaceChildren(select);

                // Apply listener for user change in value
                select.addEventListener('change', function () {
                    column
                        .search(select.value, {exact: true})
                        .draw();
                });

                // Add list of options
                column
                    .data()
                    .unique()
                    .sort()
                    .each(function (d, j) {
                        select.add(new Option(d));
                    });
            });
    }
  }
);
</script>

Is your system not included on this list?
Please [add it at the GitHub repository for this site][github]!


[github]: <https://github.com/SHAREing-dri/hpc-testbeds>
