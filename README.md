ngOnInit(): void {
  this.uploadService.gridRefreshEvent.subscribe(() => {
    console.log('[Grid Refresh] Event received');

    if (this.gridApi) {
      console.log('[Grid Refresh] Clearing server-side store cache...');
      this.gridApi.refreshServerSideStore({ purge: true });

      console.log('[Grid Refresh] Resetting server-side datasource...');
      this.gridApi.setServerSideDatasource(this.getDocumentsDataSource());

      console.log('[Grid Refresh] Done ✅');
    } else {
      console.warn('[Grid Refresh] gridApi not ready yet ❌');
    }
  });
}        this.gridApi.setServerSideDatasource(datasource);
      } else {
        // 🔁 Otherwise just refresh cache (faster, keeps scroll state)
        this.gridApi.refreshServerSideStore({ purge: true });
      }
    }
  });
}






this.uploadService.gridRefreshEvent.subscribe(() => {
  if (this.gridApi) {
    // Re-assign the datasource (forces grid to query again, even if empty)
    this.gridApi.setServerSideDatasource(this.getDocumentsDataSource());

    // If already loaded once, refresh too
    this.gridApi.refreshServerSideStore({ purge: true });
  } else {
    // If gridApi not ready yet, wait until grid is ready
    setTimeout(() => {
      if (this.gridApi) {
        this.gridApi.setServerSideDatasource(this.getDocumentsDataSource());
      }
    }, 100);
  }
});
