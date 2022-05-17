PG Prefix Search
================

Text search by word fragments using Postgres-specific indices.

Example usage::

    # in models.py
    class SearchableModel(models.Model):
        name = models.CharField('Nazwa', max_length=1024)

        class Meta:
            indexes = (
                GinIndex(text_searchable_index_spec('name'), name='searchable_model_name__gin'),
            )

    # when filtering
    queryset = SearchableModel.objects.filter(...)
    queryset = apply_search_by_name(queryset, 'name', 'rej krow gosp')
