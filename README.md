# Contabilidad
Ingresos y Gastos
<meta charset="UTF-8">
<title>SISTEMA CONTABLE - Oratorio Virgen de F&#xe1;tima</title>
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">
<link href="https://cdn.jsdelivr.net/npm/@fortawesome/fontawesome-free/css/all.min.css" rel="stylesheet">
<style>
  .sidebar {
    background: #2c3e50;
    color: white;
    min-height: 100vh;
  }
  .nav-link {
    color: white;
  }
  .nav-link:hover {
    background: #34495e;
    color: #ecf0f1;
  }
  .main-content {
    padding: 20px;
  }
  .cuenta-item {
    cursor: pointer;
    padding: 8px;
    margin: 4px 0;
    border-radius: 4px;
  }
  .cuenta-item:hover {
    background: #f8f9fa;
  }
  .content-section {
    display: none;
  }
  .partida-row {
    background: #f8f9fa;
    padding: 10px;
    margin-bottom: 10px;
    border-radius: 4px;
  }
  .main-container {
    display: none;
  }

  @media print {
    body * {
      visibility: hidden;
    }
    
    #reporteContent, #reporteContent * {
      visibility: visible;
    }
    
    #reporteContent {
      position: absolute;
      left: 0;
      top: 0;
      width: 8.5in;
      padding: 0.5in;
    }
    
    #reporteContent .card {
      border: none;
      box-shadow: none;
    }

    #reporteContent table {
      page-break-inside: auto;
    }

    #reporteContent tr {
      page-break-inside: avoid;
      page-break-after: auto;
    }

    #reporteContent thead {
      display: table-header-group;
    }

    #reporteContent tfoot {
      display: table-footer-group;
    }

    @page {
      size: letter;
      margin: 0;
    }
  }
</style>
</head>
<body>

<div id="loginContainer" class="container mt-5">
  <div class="row justify-content-center">
    <div class="col-md-6">
      <div class="card">
        <div class="card-body">
          <h3 class="text-center mb-4">Iniciar Sesi&#xf3;n</h3>
          <form id="loginForm">
            <div class="mb-3">
              <label class="form-label">Usuario</label>
              <input type="text" class="form-control" id="username" required>
            </div>
            <div class="mb-3">
              <label class="form-label">Contrase&#xf1;a</label>
              <input type="password" class="form-control" id="password" required>
            </div>
            <button type="button" class="btn btn-primary w-100" onclick="login()">
              Ingresar
            </button>
          </form>
        </div>
      </div>
    </div>
  </div>
</div>

<div class="container-fluid" style="display: none;">
  <div class="row">
    <!-- Sidebar -->
    <div class="col-md-2 sidebar p-3">
      <h4 class="text-center mb-4" id="oratorioNombre">SISTEMA CONTABLE</h4>
      <nav class="nav flex-column">
        <a class="nav-link" href="javascript:void(0)" onclick="showSection(&apos;catalogo&apos;)">
          <i class="fas fa-book"></i> Cat&#xe1;logo Contable
        </a>
        <a class="nav-link" href="javascript:void(0)" onclick="showSection(&apos;centrosCosto&apos;)">
          <i class="fas fa-sitemap"></i> Centros de Costo
        </a>
        <a class="nav-link" href="javascript:void(0)" onclick="showSection(&apos;documentos&apos;)">
          <i class="fas fa-file-alt"></i> Documentos
        </a>
        <a class="nav-link" href="javascript:void(0)" onclick="showSection(&apos;transacciones&apos;)">
          <i class="fas fa-exchange-alt"></i> Transacciones
        </a>
        <a class="nav-link" href="javascript:void(0)" onclick="showSection(&apos;reportes&apos;)">
          <i class="fas fa-chart-bar"></i> Reportes
        </a>
        <a class="nav-link" href="javascript:void(0)" onclick="showSection(&apos;parametros&apos;)">
          <i class="fas fa-cogs"></i> Par&#xe1;metros
        </a>
        <a class="nav-link text-danger" href="javascript:void(0)" onclick="logout()">
          <i class="fas fa-sign-out-alt"></i> Cerrar Sesi&#xf3;n
        </a>
      </nav>
    </div>

    <!-- Main Content -->
    <div class="col-md-10 main-content">
      <!-- Catálogo Contable -->
      <div id="catalogo" class="content-section">
        <h3>Cat&#xe1;logo de Cuentas</h3>
        <div class="row mb-3">
          <div class="col">
            <button class="btn btn-primary" onclick="showModal(&apos;nuevaCuenta&apos;)">
              <i class="fas fa-plus"></i> Nueva Cuenta
            </button>
          </div>
        </div>
        <div class="row">
          <div class="col">
            <div class="card">
              <div class="card-body">
                <div id="catalogoTree">
                  <!-- This will be populated dynamically -->
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Centros de Costo -->
      <div id="centrosCosto" class="content-section">
        <h3>Centros de Costo</h3>
        <div class="row mb-3">
          <div class="col">
            <button class="btn btn-primary" onclick="showModal(&apos;nuevoCentro&apos;)">
              <i class="fas fa-plus"></i> Nuevo Centro de Costo
            </button>
          </div>
        </div>
        <div class="table-responsive">
          <table class="table">
            <thead>
              <tr>
                <th>C&#xf3;digo</th>
                <th>Nombre</th>
                <th>Descripci&#xf3;n</th>
                <th>Acciones</th>
              </tr>
            </thead>
            <tbody>
              <!-- This will be populated dynamically -->
            </tbody>
          </table>
        </div>
      </div>

      <!-- Documentos -->
      <div id="documentos" class="content-section">
        <h3>Configuraci&#xf3;n de Documentos</h3>
        <div class="row mb-3">
          <div class="col">
            <button class="btn btn-primary" onclick="showModal(&apos;nuevoDocumento&apos;)">
              <i class="fas fa-plus"></i> Nuevo Tipo de Documento
            </button>
          </div>
        </div>
        <div class="table-responsive">
          <table class="table">
            <thead>
              <tr>
                <th>C&#xf3;digo</th>
                <th>Tipo de Documento</th>
                <th>Partidas Autom&#xe1;ticas</th>
                <th>Acciones</th>
              </tr>
            </thead>
            <tbody>
              <!-- This will be populated dynamically -->
            </tbody>
          </table>
        </div>
      </div>

      <!-- Transacciones -->
      <div id="transacciones" class="content-section">
        <h3>Transacciones</h3>
        <div class="row mb-3">
          <div class="col">
            <button class="btn btn-primary" onclick="showModal(&apos;nuevaTransaccion&apos;)">
              <i class="fas fa-plus"></i> Nueva Transacci&#xf3;n
            </button>
          </div>
        </div>
        <div class="table-responsive">
          <table class="table">
            <thead>
              <tr>
                <th>Fecha</th>
                <th>Documento</th>
                <th>Descripci&#xf3;n</th>
                <th>Total DB</th>
                <th>Total CR</th>
                <th>Acciones</th>
              </tr>
            </thead>
            <tbody id="transaccionesTableBody">
              <!-- This will be populated dynamically -->
            </tbody>
          </table>
        </div>
      </div>

      <!-- Reportes -->
      <div id="reportes" class="content-section">
        <h3>Reportes</h3>
        <div class="row mb-3">
          <div class="col-md-4">
            <div class="card">
              <div class="card-body">
                <h5 class="card-title">Libro Diario</h5>
                <div class="mb-3">
                  <label class="form-label">Rango de Fechas</label>
                  <input type="date" class="form-control mb-2" id="libroDiarioDesde">
                  <input type="date" class="form-control" id="libroDiarioHasta">
                </div>
                <button class="btn btn-primary" onclick="generarLibroDiario()">
                  <i class="fas fa-book"></i> Generar Reporte
                </button>
              </div>
            </div>
          </div>
          
          <div class="col-md-4">
            <div class="card">
              <div class="card-body">
                <h5 class="card-title">Libro Mayor</h5>
                <div class="mb-3">
                  <label class="form-label">Cuenta</label>
                  <select class="form-select mb-2" id="libroMayorCuenta">
                    <option value>-- Seleccione una cuenta --</option>
                  </select>
                </div>
                <div class="mb-3">
                  <label class="form-label">Rango de Fechas</label>
                  <input type="date" class="form-control mb-2" id="libroMayorDesde">
                  <input type="date" class="form-control" id="libroMayorHasta">
                </div>
                <button class="btn btn-primary" onclick="generarLibroMayor()">
                  <i class="fas fa-book-open"></i> Generar Reporte
                </button>
              </div>
            </div>
          </div>

          <div class="col-md-4">
            <div class="card">
              <div class="card-body">
                <h5 class="card-title">Ingresos y Gastos</h5>
                <div class="mb-3">
                  <label class="form-label">Rango de Fechas</label>
                  <input type="date" class="form-control mb-2" id="ingresosGastosDesde">
                  <input type="date" class="form-control" id="ingresosGastosHasta">
                </div>
                <button class="btn btn-primary" onclick="generarIngresosGastos()">
                  <i class="fas fa-chart-line"></i> Generar Reporte
                </button>
              </div>
            </div>
          </div>
          <div class="col-md-4">
            <div class="card">
              <div class="card-body">
                <h5 class="card-title">Reporte por Centro de Costo</h5>
                <div class="mb-3">
                  <label class="form-label">Centro de Costo</label>
                  <select class="form-select" id="centroCostoReporte">
                    <option value>-- Todos los Centros --</option>
                  </select>
                  <label class="form-label">Rango de Fechas</label>
                  <input type="date" class="form-control mb-2" id="centroCostoDesde">
                  <input type="date" class="form-control" id="centroCostoHasta">
                </div>
                <button class="btn btn-primary" onclick="generarReporteCentroCosto()">
                  <i class="fas fa-building"></i> Generar Reporte
                </button>
              </div>
            </div>
          </div>
          <div class="col-md-4">
            <div class="card">
              <div class="card-body">
                <h5 class="card-title">Cierre de Mes</h5>
                <div class="mb-3">
                  <label class="form-label">Mes a Cerrar</label>
                  <input type="month" class="form-control mb-2" id="mesCierre" min max>
                </div>
                <div class="mb-3">
                  <label class="form-label">Centro de Costo</label>
                  <select class="form-select" id="centroCostoCierre">
                    <option value>-- Ninguno --</option>
                  </select>
                </div>
                <button class="btn btn-primary" onclick="cerrarMes()">
                  <i class="fas fa-lock"></i> Cerrar Mes
                </button>
              </div>
            </div>
          </div>
          <div class="col-md-4">
            <div class="card">
              <div class="card-body">
                <h5 class="card-title">Partidas Manuales</h5>
                <div class="mb-3">
                  <label class="form-label">Fecha</label>
                  <input type="date" class="form-control mb-2" id="fechaPartidaManual">
                </div>
                <div class="mb-3">
                  <label class="form-label">Descripci&#xf3;n</label>
                  <input type="text" class="form-control" id="descripcionPartidaManual">
                </div>
                <button class="btn btn-primary" onclick="nuevaPartidaManual()">
                  <i class="fas fa-plus"></i> Nueva Partida Manual
                </button>
              </div>
            </div>
          </div>
        </div>
        <div class="col-md-4">
          <div class="card">
            <div class="card-body">
              <h5 class="card-title">Balance General</h5>
              <div class="mb-3">
                <label class="form-label">Al d&#xed;a</label>
                <input type="date" class="form-control mb-2" id="fechaBalance">
              </div>
              <button class="btn btn-primary" onclick="generarBalanceGeneral()">
                <i class="fas fa-balance-scale"></i> Generar Balance
              </button>
            </div>
          </div>
        </div>
        <div id="reporteContent" class="mt-4">
          <!-- Report content will be displayed here -->
        </div>
      </div>

      <!-- Parámetros -->
      <div id="parametros" class="content-section">
        <h3>Par&#xe1;metros del Sistema</h3>
        <div class="row">
          <div class="col-md-6">
            <div class="card">
              <div class="card-body">
                <h5>Informaci&#xf3;n General</h5>
                <form id="parametrosForm">
                  <div class="mb-3">
                    <label class="form-label">Nombre del Oratorio</label>
                    <input type="text" class="form-control" id="nombreOratorio">
                  </div>
                  <div class="mb-3">
                    <label class="form-label">Direcci&#xf3;n</label>
                    <input type="text" class="form-control" id="direccionOratorio">
                  </div>
                  <div class="mb-3">
                    <label class="form-label">Tel&#xe9;fono</label>
                    <input type="text" class="form-control" id="telefonoOratorio">
                  </div>
                  <div class="mb-3">
                    <label class="form-label">Email</label>
                    <input type="email" class="form-control" id="emailOratorio">
                  </div>
                  <div class="mb-3">
                    <label class="form-label">Coordinador Responsable</label>
                    <input type="text" class="form-control" id="coordinadorOratorio">
                  </div>
                  <div class="mb-3">
                    <label class="form-label">Tesorero</label>
                    <input type="text" class="form-control" id="tesoreroOratorio">
                  </div>
                  <div class="mb-3"> 
                    <label class="form-label">Logotipo</label>
                    <input type="file" class="form-control" id="logoOratorio" accept="image/*">
                    <div id="logoPreview" class="mt-2 text-center">
                      <!-- Logo preview will show here -->
                    </div>
                  </div>
                  <button type="button" class="btn btn-primary" onclick="guardarParametros()">
                    <i class="fas fa-save"></i> Guardar Cambios
                  </button>
                </form>
              </div>
            </div>
          </div>
        </div>
        <div class="row mt-4" id="backupSection">
          <div class="col-md-6">
            <div class="card">
              <div class="card-body">
                <h5>Copias de Seguridad</h5>
                <div class="mb-3">
                  <button class="btn btn-primary" onclick="crearBackup()">
                    <i class="fas fa-download"></i> Crear Copia de Seguridad
                  </button>
                </div>
                <div class="mb-3">
                  <label class="form-label">Restaurar Copia de Seguridad</label>
                  <input type="file" class="form-control" id="backupFile" accept=".json">
                </div>
                <button class="btn btn-warning" onclick="restaurarBackup()">
                  <i class="fas fa-upload"></i> Restaurar Backup
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>

<!-- Modales -->
<div class="modal fade" id="nuevaCuenta" tabindex="-1">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title">Nueva Cuenta Contable</h5>
        <button type="button" class="btn-close" data-bs-dismiss="modal"></button>
      </div>
      <div class="modal-body">
        <form id="cuentaForm">
          <div class="mb-3">
            <label class="form-label">C&#xf3;digo</label>
            <input type="text" name="codigo" class="form-control" required>
          </div>
          <div class="mb-3">
            <label class="form-label">Nombre</label>
            <input type="text" name="nombre" class="form-control" required>
          </div>
          <div class="mb-3">
            <label class="form-label">Tipo</label>
            <select name="tipo" class="form-select" required>
              <option value="activo">Activo</option>
              <option value="pasivo">Pasivo</option>
              <option value="capital">Capital</option>
              <option value="ingreso">Ingreso</option>
              <option value="gasto">Gasto</option>
            </select>
          </div>
          <div class="mb-3">
            <label class="form-label">Cuenta Padre (opcional)</label>
            <select name="padre" class="form-select">
              <option value>-- Seleccione --</option>
            </select>
          </div>
          <div class="mb-3">
            <label class="form-label">Centro de Costo</label>
            <select name="centroCosto" class="form-select" id="centroCostoSelect">
              <option value>-- Ninguno --</option>
            </select>
          </div>
        </form>
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Cerrar</button>
        <button type="button" class="btn btn-primary" id="guardarCuentaBtn">
          Guardar
        </button>
      </div>
    </div>
  </div>
</div>

<div class="modal fade" id="nuevoCentro" tabindex="-1">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title">Nuevo Centro de Costo</h5>
        <button type="button" class="btn-close" data-bs-dismiss="modal"></button>
      </div>
      <div class="modal-body">
        <form id="centroForm">
          <div class="mb-3">
            <label class="form-label">C&#xf3;digo</label>
            <input type="text" class="form-control" required>
          </div>
          <div class="mb-3">
            <label class="form-label">Nombre</label>
            <input type="text" class="form-control" required>
          </div>
          <div class="mb-3">
            <label class="form-label">Descripci&#xf3;n</label>
            <input type="text" class="form-control" required>
          </div>
        </form>
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Cerrar</button>
        <button type="button" class="btn btn-primary" onclick="guardarCentro()">Guardar</button>
      </div>
    </div>
  </div>
</div>

<div class="modal fade" id="nuevoDocumento" tabindex="-1">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title">Nuevo Tipo de Documento</h5>
        <button type="button" class="btn-close" data-bs-dismiss="modal"></button>
      </div>
      <div class="modal-body">
        <form id="documentoForm">
          <div class="mb-3">
            <label class="form-label">C&#xf3;digo</label>
            <input type="text" name="codigo" class="form-control" required>
          </div>
          <div class="mb-3">
            <label class="form-label">Nombre</label>
            <input type="text" name="nombre" class="form-control" required>
          </div>
          <div id="partidasContainer">
            <div class="partida-row">
              <h6>Partida 1</h6>
              <div class="row">
                <div class="col-md-6">
                  <label class="form-label">Cuenta</label>
                  <select name="cuenta[]" class="form-select cuenta-select" required>
                    <option value>Seleccione cuenta...</option>
                  </select>
                </div>
                <div class="col-md-6">
                  <label class="form-label">Tipo</label>
                  <select name="tipo[]" class="form-select" required>
                    <option value="DB">D&#xe9;bito</option>
                    <option value="CR">Cr&#xe9;dito</option>
                  </select>
                </div>
              </div>
            </div>
          </div>
          <button type="button" class="btn btn-secondary mt-2" onclick="agregarPartida()">
            <i class="fas fa-plus"></i> Agregar Partida
          </button>
        </form>
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Cerrar</button>
        <button type="button" class="btn btn-primary" onclick="guardarDocumento()">Guardar</button>
      </div>
    </div>
  </div>
</div>

<!-- Nueva Transacción Modal -->
<div class="modal fade" id="nuevaTransaccion" tabindex="-1">
  <div class="modal-dialog modal-lg">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title">Nueva Transacci&#xf3;n</h5>
        <button type="button" class="btn-close" data-bs-dismiss="modal"></button>
      </div>
      <div class="modal-body">
        <form id="transaccionForm">
          <div class="row mb-3">
            <div class="col-md-6">
              <label class="form-label">Fecha</label>
              <input type="date" class="form-control" id="fechaTransaccion" required>
            </div>
            <div class="col-md-6">
              <label class="form-label">Tipo de Documento</label>
              <select class="form-select" id="tipoDocumento">
                <option value>Seleccione...</option>
              </select>
            </div>
          </div>
          <div class="mb-3">
            <label class="form-label">Centro de Costo</label> 
            <select class="form-select" id="centroCostoTransaccion">
              <option value>-- Ninguno --</option>
            </select>
          </div>
          <div class="mb-3">
            <label class="form-label">Descripci&#xf3;n</label>
            <input type="text" class="form-control" id="descripcionTransaccion" required>
          </div>
          <div class="mb-3">
            <label class="form-label">Monto</label>
            <input type="number" class="form-control" id="montoTransaccion" step="0.01" required>
          </div>
        </form>
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Cerrar</button>
        <button type="button" class="btn btn-primary" onclick="guardarTransaccion()">Guardar</button>
      </div>
    </div>
  </div>
</div>

<!-- Editar Transacción Modal -->
<div class="modal fade" id="editarTransaccion" tabindex="-1">
  <div class="modal-dialog modal-lg">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title">Editar Transacci&#xf3;n</h5>
        <button type="button" class="btn-close" data-bs-dismiss="modal"></button>
      </div>
      <div class="modal-body">
        <form id="editTransaccionForm">
          <input type="hidden" id="editTransaccionIndex">
          <div class="row mb-3">
            <div class="col-md-6">
              <label class="form-label">Fecha</label>
              <input type="date" class="form-control" id="editFechaTransaccion" required>
            </div>
            <div class="col-md-6">
              <label class="form-label">Tipo de Documento</label>
              <select class="form-select" id="editTipoDocumento">
                <option value>Seleccione...</option>
              </select>
            </div>
          </div>
          <div class="mb-3">
            <label class="form-label">Centro de Costo</label>
            <select class="form-select" id="editCentroCostoTransaccion">
              <option value>-- Ninguno --</option>
            </select>
          </div>
          <div class="mb-3">
            <label class="form-label">Descripci&#xf3;n</label>
            <input type="text" class="form-control" id="editDescripcionTransaccion" required>
          </div>
          <div class="mb-3">
            <label class="form-label">Monto</label>
            <input type="number" class="form-control" id="editMontoTransaccion" step="0.01" required>
          </div>
        </form>
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Cerrar</button>
        <button type="button" class="btn btn-primary" onclick="actualizarTransaccion()">Guardar Cambios</button>
      </div>
    </div>
  </div>
</div>

<!-- Editar Cuenta Modal -->
<div class="modal fade" id="editarCuenta" tabindex="-1">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title">Editar Cuenta Contable</h5>
        <button type="button" class="btn-close" data-bs-dismiss="modal"></button>
      </div>
      <div class="modal-body">
        <form id="editCuentaForm">
          <input type="hidden" id="editCuentaIndex">
          <div class="mb-3">
            <label class="form-label">C&#xf3;digo</label>
            <input type="text" name="codigo" class="form-control" id="editCuentaCodigo" required>
          </div>
          <div class="mb-3">
            <label class="form-label">Nombre</label>
            <input type="text" name="nombre" class="form-control" id="editCuentaNombre" required>
          </div>
          <div class="mb-3">
            <label class="form-label">Tipo</label>
            <select name="tipo" class="form-select" id="editCuentaTipo" required>
              <option value="activo">Activo</option>
              <option value="pasivo">Pasivo</option>
              <option value="capital">Capital</option>
              <option value="ingreso">Ingreso</option>
              <option value="gasto">Gasto</option>
            </select>
          </div>
          <div class="mb-3">
            <label class="form-label">Cuenta Padre (opcional)</label>
            <select name="padre" class="form-select" id="editCuentaPadre">
              <option value>-- Seleccione --</option>
            </select>
          </div>
          <div class="mb-3">
            <label class="form-label">Centro de Costo</label>
            <select name="centroCosto" class="form-select" id="editCentroCostoSelect">
              <option value>-- Ninguno --</option>
            </select>
          </div>
        </form>
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Cerrar</button>
        <button type="button" class="btn btn-primary" onclick="actualizarCuenta()">Guardar Cambios</button>
      </div>
    </div>
  </div>
</div>

<div class="modal fade" id="distribucionSaldo" tabindex="-1">
  <div class="modal-dialog modal-lg">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title">Distribuir Saldo entre Centros de Costo</h5>
        <button type="button" class="btn-close" data-bs-dismiss="modal"></button>
      </div>
      <div class="modal-body">
        <p>Saldo total a distribuir: <span id="saldoTotalDistribuir"></span></p>
        <div class="table-responsive">
          <table class="table" id="distribucionTable">
            <thead>
              <tr>
                <th>Centro de Costo</th>
                <th>Monto</th>
              </tr>
            </thead>
            <tbody>
            </tbody>
            <tfoot>
              <tr>
                <th>Total Distribuido</th>
                <td id="totalDistribuido">0.00</td>
              </tr>
            </tfoot>
          </table>
        </div>
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Cancelar</button>
        <button type="button" class="btn btn-primary" onclick="confirmarDistribucion()">Confirmar</button>
      </div>
    </div>
  </div>
</div>

<div class="modal fade" id="partidaManualModal" tabindex="-1">
  <div class="modal-dialog modal-lg">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title">Nueva Partida Manual</h5>
        <button type="button" class="btn-close" data-bs-dismiss="modal"></button>
      </div>
      <div class="modal-body">
        <div class="row mb-3">
          <div class="col">
            <button class="btn btn-secondary" onclick="agregarLineaPartida()">
              <i class="fas fa-plus"></i> Agregar l&#xed;nea
            </button>
          </div>
        </div>
        <form id="partidaManualForm">
          <div id="lineasPartida">
            <!-- Lines will be added dynamically -->
          </div>
        </form>
      </div>
      <div class="modal-footer">
        <div class="container-fluid">
          <div class="row">
            <div class="col text-start">
              <span>Total D&#xe9;bito: <strong id="totalDebito">0.00</strong></span>
            </div>
            <div class="col text-center">
              <span>Total Cr&#xe9;dito: <strong id="totalCredito">0.00</strong></span>
            </div>
            <div class="col text-end">
              <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Cerrar</button>
              <button type="button" class="btn btn-primary" onclick="guardarPartidaManual()">Guardar</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>

<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js"></script>
<script>const USERS = {
  Administrador: {
    password: '1977362013',
    role: 'admin'
  },
  Gloria: {
    password: '123456',
    role: 'colaborador'
  }
};
let currentUser = null;
function login() {
  const username = document.getElementById('username').value;
  const password = document.getElementById('password').value;
  const user = USERS[username];
  if (user && user.password === password) {
    currentUser = {
      username,
      role: user.role
    };
    document.getElementById('loginContainer').style.display = 'none';
    document.querySelector('.container-fluid').style.display = 'block';
    if (user.role === 'colaborador') {
      const restrictedMenus = ['catalogo', 'centrosCosto', 'documentos', 'parametros'];
      restrictedMenus.forEach(menu => {
        document.querySelector(`[onclick="showSection('${menu}')"]`).style.display = 'none';
      });
    }
    showSection('transacciones');
  } else {
    alert('Usuario o contraseña incorrectos');
  }
}
function checkAccess(section) {
  if (!currentUser) return false;
  if (currentUser.role === 'admin') return true;
  if (currentUser.role === 'colaborador') {
    return ['transacciones', 'reportes'].includes(section);
  }
  return false;
}
function showSection(sectionId) {
  if (!checkAccess(sectionId)) {
    alert('No tiene permiso para acceder a esta sección');
    return;
  }
  document.querySelectorAll('.content-section').forEach(section => {
    section.style.display = 'none';
  });
  const section = document.getElementById(sectionId);
  if (section) {
    section.style.display = 'block';
  }
}
function populateDocumentTypes() {
  const documentos = JSON.parse(localStorage.getItem('documentos') || '[]');
  const select = document.getElementById('tipoDocumento');
  select.innerHTML = '<option value="">Seleccione...</option>';
  documentos.forEach(doc => {
    const option = document.createElement('option');
    option.value = doc.codigo;
    option.textContent = `${doc.codigo} - ${doc.nombre}`;
    select.appendChild(option);
  });
}
function guardarTransaccion() {
  const fecha = document.getElementById('fechaTransaccion').value;
  const tipoDoc = document.getElementById('tipoDocumento').value;
  const descripcion = document.getElementById('descripcionTransaccion').value;
  const monto = parseFloat(document.getElementById('montoTransaccion').value);
  const centroCosto = document.getElementById('centroCostoTransaccion').value;
  if (!fecha || !tipoDoc || !descripcion || !monto) {
    alert('Por favor complete todos los campos');
    return;
  }
  const documentos = JSON.parse(localStorage.getItem('documentos') || '[]');
  const docConfig = documentos.find(d => d.codigo === tipoDoc);
  if (!docConfig) {
    alert('Tipo de documento no encontrado');
    return;
  }
  const transaccion = {
    fecha,
    tipoDocumento: tipoDoc,
    descripcion,
    monto,
    centroCosto,
    partidas: docConfig.partidas.map(p => ({
      cuenta: p.cuenta,
      tipo: p.tipo,
      monto: monto,
      centroCosto
    })),
    fechaCreacion: new Date().toISOString()
  };
  let transacciones = JSON.parse(localStorage.getItem('transacciones') || '[]');
  transacciones.push(transaccion);
  localStorage.setItem('transacciones', JSON.stringify(transacciones));
  actualizarTablaTransacciones();
  const modal = bootstrap.Modal.getInstance(document.getElementById('nuevaTransaccion'));
  modal.hide();
  document.getElementById('transaccionForm').reset();
}
function actualizarTablaTransacciones() {
  const transaccionesBackup = JSON.parse(localStorage.getItem('transaccionesBackup') || '[]');
  const transacciones = [...JSON.parse(localStorage.getItem('transacciones') || '[]')];
  transacciones.push(...transaccionesBackup.filter(t => !transacciones.find(et => et.fecha === t.fecha && et.descripcion === t.descripcion && et.monto === t.monto)));
  const tbody = document.getElementById('transaccionesTableBody');
  tbody.innerHTML = transacciones.map((t, index) => `
    <tr>
      <td>${t.fecha}</td>
      <td>${t.tipoDocumento}</td>
      <td>${t.descripcion}${t.centroCosto ? ` <br><small>(CC: ${t.centroCosto})</small>` : ''}</td>
      <td>${t.monto.toFixed(2)}</td>
      <td>${t.monto.toFixed(2)}</td>
      <td>
        <button class="btn btn-sm btn-info" onclick="editarTransaccion(${index})">
          <i class="fas fa-edit"></i>
        </button>
        <button class="btn btn-sm btn-danger" onclick="eliminarTransaccion(${index})">
          <i class="fas fa-trash"></i>
        </button>
      </td>
    </tr>
  `).join('');
}
function populateCuentaSelects() {
  const cuentas = JSON.parse(localStorage.getItem('cuentas') || '[]');
  document.querySelectorAll('.cuenta-select').forEach(select => {
    select.innerHTML = '<option value="">Seleccione cuenta...</option>';
    cuentas.forEach(cuenta => {
      const option = document.createElement('option');
      option.value = cuenta.codigo;
      option.textContent = `${cuenta.codigo} - ${cuenta.nombre}`;
      select.appendChild(option);
    });
  });
}
function guardarDocumento() {
  const formulario = document.getElementById('documentoForm');
  const codigo = formulario.elements['codigo'].value;
  const nombre = formulario.elements['nombre'].value;
  const partidas = [];
  const cuentaSelects = formulario.querySelectorAll('.cuenta-select');
  const tipoSelects = formulario.querySelectorAll('select[name="tipo[]"]');
  for (let i = 0; i < cuentaSelects.length; i++) {
    partidas.push({
      cuenta: cuentaSelects[i].value,
      tipo: tipoSelects[i].value
    });
  }
  if (!codigo || !nombre || partidas.length === 0) {
    alert('Por favor complete todos los campos requeridos');
    return;
  }
  const hasDebit = partidas.some(p => p.tipo === 'DB');
  const hasCredit = partidas.some(p => p.tipo === 'CR');
  if (!hasDebit || !hasCredit) {
    alert('Debe incluir al menos una partida débito y una crédito');
    return;
  }
  const documento = {
    codigo,
    nombre,
    partidas,
    fechaCreacion: new Date().toISOString()
  };
  let documentos = JSON.parse(localStorage.getItem('documentos') || '[]');
  documentos.push(documento);
  localStorage.setItem('documentos', JSON.stringify(documentos));
  actualizarTablaDocumentos();
  const modal = bootstrap.Modal.getInstance(document.getElementById('nuevoDocumento'));
  modal.hide();
  formulario.reset();
  document.getElementById('partidasContainer').innerHTML = `
    <div class="partida-row">
      <h6>Partida 1</h6>
      <div class="row">
        <div class="col-md-6">
          <label class="form-label">Cuenta</label>
          <select name="cuenta[]" class="form-select cuenta-select" required>
            <option value="">Seleccione cuenta...</option>
          </select>
        </div>
        <div class="col-md-6">
          <label class="form-label">Tipo</label>
          <select name="tipo[]" class="form-select" required>
            <option value="DB">Débito</option>
            <option value="CR">Crédito</option>
          </select>
        </div>
      </div>
    </div>
  `;
  populateCuentaSelects();
}
function agregarPartida() {
  const partidasContainer = document.getElementById('partidasContainer');
  const partidaRow = document.createElement('div');
  partidaRow.className = 'partida-row';
  partidaRow.innerHTML = `
    <h6>Partida ${partidasContainer.children.length + 1}</h6>
    <div class="row">
      <div class="col-md-6">
        <label class="form-label">Cuenta</label>
        <select name="cuenta[]" class="form-select cuenta-select" required>
          <option value="">Seleccione cuenta...</option>
        </select>
      </div>
      <div class="col-md-6">
        <label class="form-label">Tipo</label>
        <select name="tipo[]" class="form-select" required>
          <option value="DB">Débito</option>
          <option value="CR">Crédito</option>
        </select>
      </div>
    </div>
  `;
  partidasContainer.appendChild(partidaRow);
  populateCuentaSelects();
}
function guardarCentro() {
  const formulario = document.getElementById('centroForm');
  const codigo = formulario.elements[0].value;
  const nombre = formulario.elements[1].value;
  const descripcion = formulario.elements[2].value;
  if (!codigo || !nombre || !descripcion) {
    alert('Por favor complete todos los campos');
    return;
  }
  const centro = {
    codigo,
    nombre,
    descripcion,
    fechaCreacion: new Date().toISOString()
  };
  let centros = JSON.parse(localStorage.getItem('centros') || '[]');
  centros.push(centro);
  localStorage.setItem('centros', JSON.stringify(centros));
  actualizarTablaCentros();
  const modal = bootstrap.Modal.getInstance(document.getElementById('nuevoCentro'));
  modal.hide();
  formulario.reset();
}
function actualizarTablaCentros() {
  const centrosBackup = JSON.parse(localStorage.getItem('centrosBackup') || '[]');
  const centros = [...JSON.parse(localStorage.getItem('centros') || '[]')];
  centros.push(...centrosBackup.filter(c => !centros.find(ec => ec.codigo === c.codigo)));
  const tbody = document.querySelector('#centrosCosto table tbody');
  tbody.innerHTML = centros.map(centro => `
    <tr>
      <td>${centro.codigo}</td>
      <td>${centro.nombre}</td>
      <td>${centro.descripcion}</td>
      <td>
        <button class="btn btn-sm btn-info"><i class="fas fa-edit"></i></button>
        <button class="btn btn-sm btn-danger" onclick="eliminarCentro('${centro.codigo}')">
          <i class="fas fa-trash"></i>
        </button>
      </td>
    </tr>
  `).join('');
}
function eliminarCentro(codigo) {
  if (confirm('¿Está seguro de eliminar este centro de costo?')) {
    let centros = JSON.parse(localStorage.getItem('centros') || '[]');
    centros = centros.filter(c => c.codigo !== codigo);
    localStorage.setItem('centros', JSON.stringify(centros));
    actualizarTablaCentros();
  }
}
function guardarCuenta() {
  const form = document.getElementById('cuentaForm');
  const cuenta = {
    codigo: form.elements['codigo'].value,
    nombre: form.elements['nombre'].value,
    tipo: form.elements['tipo'].value,
    padre: form.elements['padre'].value,
    centroCosto: form.elements['centroCosto'].value,
    fechaCreacion: new Date().toISOString()
  };
  if (!cuenta.codigo || !cuenta.nombre || !cuenta.tipo) {
    alert('Por favor complete los campos requeridos');
    return;
  }
  let cuentas = JSON.parse(localStorage.getItem('cuentas') || '[]');
  cuentas.push(cuenta);
  localStorage.setItem('cuentas', JSON.stringify(cuentas));
  actualizarCatalogo();
  populateCuentaSelects();
  const modal = bootstrap.Modal.getInstance(document.getElementById('nuevaCuenta'));
  modal.hide();
  form.reset();
}
function actualizarCatalogo() {
  const cuentas = JSON.parse(localStorage.getItem('cuentas') || '[]');
  const cuentasBackup = JSON.parse(localStorage.getItem('cuentasBackup') || '[]');
  cuentas.push(...cuentasBackup.filter(c => !cuentas.find(ec => ec.codigo === c.codigo)));
  const catalogoTree = document.getElementById('catalogoTree');
  catalogoTree.innerHTML = '';
  function buildTree(cuenta) {
    const div = document.createElement('div');
    div.className = 'cuenta-item';
    const centroCosto = cuenta.centroCosto ? ` (CC: ${cuenta.centroCosto})` : '';
    div.innerHTML = `
      <i class="fas fa-${cuenta.hijos ? 'folder' : 'file'}"></i>
      ${cuenta.codigo} - ${cuenta.nombre}${centroCosto}
      <button class="btn btn-sm btn-info float-end" onclick="editarCuenta('${cuenta.codigo}')">
        <i class="fas fa-edit"></i>
      </button>
    `;
    if (cuenta.hijos) {
      const subDiv = document.createElement('div');
      subDiv.className = 'ms-4';
      cuenta.hijos.forEach(hijo => {
        subDiv.appendChild(buildTree(hijo));
      });
      div.appendChild(subDiv);
    }
    return div;
  }
  const buildTreeStructure = cuentas => {
    const tree = {};
    cuentas.forEach(cuenta => {
      if (!cuenta.padre) {
        if (!tree[cuenta.codigo]) {
          tree[cuenta.codigo] = {
            ...cuenta,
            hijos: []
          };
        }
      } else {
        const padre = findParent(tree, cuenta.padre);
        if (padre) {
          padre.hijos.push({
            ...cuenta
          });
        }
      }
    });
    return Object.values(tree);
  };
  const findParent = (tree, codigo) => {
    for (const key in tree) {
      if (tree[key].codigo === codigo) return tree[key];
      if (tree[key].hijos) {
        const found = findParent(tree[key].hijos, codigo);
        if (found) return found;
      }
    }
    return null;
  };
  const treeData = buildTreeStructure(cuentas);
  treeData.forEach(cuenta => {
    catalogoTree.appendChild(buildTree(cuenta));
  });
}
function editarTransaccion(index) {
  const transacciones = JSON.parse(localStorage.getItem('transacciones') || '[]');
  const transaccion = transacciones[index];
  populateDocumentTypes();
  const centros = JSON.parse(localStorage.getItem('centros') || '[]');
  const select = document.getElementById('editCentroCostoTransaccion');
  select.innerHTML = '<option value="">-- Ninguno --</option>';
  centros.forEach(centro => {
    const option = document.createElement('option');
    option.value = centro.codigo;
    option.textContent = `${centro.codigo} - ${centro.nombre}`;
    select.appendChild(option);
  });
  document.getElementById('editTransaccionIndex').value = index;
  document.getElementById('editFechaTransaccion').value = transaccion.fecha;
  document.getElementById('editTipoDocumento').value = transaccion.tipoDocumento;
  document.getElementById('editCentroCostoTransaccion').value = transaccion.centroCosto || '';
  document.getElementById('editDescripcionTransaccion').value = transaccion.descripcion;
  document.getElementById('editMontoTransaccion').value = transaccion.monto;
  const modal = new bootstrap.Modal(document.getElementById('editarTransaccion'));
  modal.show();
}
function actualizarTransaccion() {
  const index = parseInt(document.getElementById('editTransaccionIndex').value);
  const fecha = document.getElementById('editFechaTransaccion').value;
  const tipoDoc = document.getElementById('editTipoDocumento').value;
  const descripcion = document.getElementById('editDescripcionTransaccion').value;
  const monto = parseFloat(document.getElementById('editMontoTransaccion').value);
  const centroCosto = document.getElementById('editCentroCostoTransaccion').value;
  if (!fecha || !tipoDoc || !descripcion || !monto) {
    alert('Por favor complete todos los campos');
    return;
  }
  const documentos = JSON.parse(localStorage.getItem('documentos') || '[]');
  const docConfig = documentos.find(d => d.codigo === tipoDoc);
  if (!docConfig) {
    alert('Tipo de documento no encontrado');
    return;
  }
  const transaccion = {
    fecha,
    tipoDocumento: tipoDoc,
    descripcion,
    monto,
    centroCosto,
    partidas: docConfig.partidas.map(p => ({
      cuenta: p.cuenta,
      tipo: p.tipo,
      monto: monto,
      centroCosto
    })),
    fechaCreacion: new Date().toISOString()
  };
  let transacciones = JSON.parse(localStorage.getItem('transacciones') || '[]');
  transacciones[index] = transaccion;
  localStorage.setItem('transacciones', JSON.stringify(transacciones));
  actualizarTablaTransacciones();
  const modal = bootstrap.Modal.getInstance(document.getElementById('editarTransaccion'));
  modal.hide();
  document.getElementById('editTransaccionForm').reset();
}
function eliminarTransaccion(index) {
  if (confirm('¿Está seguro de eliminar esta transacción?')) {
    let transacciones = JSON.parse(localStorage.getItem('transacciones') || '[]');
    transacciones.splice(index, 1);
    localStorage.setItem('transacciones', JSON.stringify(transacciones));
    actualizarTablaTransacciones();
  }
}
function editarCuenta(codigo) {
  const cuentas = JSON.parse(localStorage.getItem('cuentas') || '[]');
  const index = cuentas.findIndex(c => c.codigo === codigo);
  const cuenta = cuentas[index];
  const centros = JSON.parse(localStorage.getItem('centros') || '[]');
  const selectCentro = document.getElementById('editCentroCostoSelect');
  selectCentro.innerHTML = '<option value="">-- Ninguno --</option>';
  centros.forEach(centro => {
    const option = document.createElement('option');
    option.value = centro.codigo;
    option.textContent = `${centro.codigo} - ${centro.nombre}`;
    selectCentro.appendChild(option);
  });
  const selectPadre = document.getElementById('editCuentaPadre');
  selectPadre.innerHTML = '<option value="">-- Seleccione --</option>';
  cuentas.forEach(c => {
    if (c.codigo !== codigo) {
      const option = document.createElement('option');
      option.value = c.codigo;
      option.textContent = `${c.codigo} - ${c.nombre}`;
      selectPadre.appendChild(option);
    }
  });
  document.getElementById('editCuentaIndex').value = index;
  document.getElementById('editCuentaCodigo').value = cuenta.codigo;
  document.getElementById('editCuentaNombre').value = cuenta.nombre;
  document.getElementById('editCuentaTipo').value = cuenta.tipo;
  document.getElementById('editCuentaPadre').value = cuenta.padre || '';
  document.getElementById('editCentroCostoSelect').value = cuenta.centroCosto || '';
  const modal = new bootstrap.Modal(document.getElementById('editarCuenta'));
  modal.show();
}
function actualizarCuenta() {
  const index = parseInt(document.getElementById('editCuentaIndex').value);
  const form = document.getElementById('editCuentaForm');
  const cuentaActualizada = {
    codigo: form.elements['codigo'].value,
    nombre: form.elements['nombre'].value,
    tipo: form.elements['tipo'].value,
    padre: form.elements['padre'].value,
    centroCosto: form.elements['centroCosto'].value,
    fechaCreacion: new Date().toISOString()
  };
  if (!cuentaActualizada.codigo || !cuentaActualizada.nombre || !cuentaActualizada.tipo) {
    alert('Por favor complete los campos requeridos');
    return;
  }
  let cuentas = JSON.parse(localStorage.getItem('cuentas') || '[]');
  cuentas[index] = cuentaActualizada;
  localStorage.setItem('cuentas', JSON.stringify(cuentas));
  actualizarCatalogo();
  const modal = bootstrap.Modal.getInstance(document.getElementById('editarCuenta'));
  modal.hide();
  form.reset();
}
function generarReporteCentroCosto() {
  const centroCosto = document.getElementById('centroCostoReporte').value;
  const desde = document.getElementById('centroCostoDesde').value;
  const hasta = document.getElementById('centroCostoHasta').value;
  if (!desde || !hasta) {
    alert('Por favor complete las fechas');
    return;
  }
  const parametros = JSON.parse(localStorage.getItem('parametrosOratorio') || '{}');
  const transacciones = JSON.parse(localStorage.getItem('transacciones') || '[]');
  const centros = JSON.parse(localStorage.getItem('centros') || '[]');
  const getCentroNombre = codigo => {
    const centro = centros.find(c => c.codigo === codigo);
    return centro ? `${centro.nombre}` : 'Sin Centro';
  };
  const transaccionesFiltradas = transacciones.filter(t => {
    const fecha = new Date(t.fecha);
    return fecha >= new Date(desde) && fecha <= new Date(hasta) && (centroCosto === '' || t.centroCosto === centroCosto);
  });
  let totalIngresos = 0;
  let totalGastos = 0;
  let detalleTransacciones = [];
  const centrosDeCosto = new Set();
  const resultadosPorCentro = {};
  transaccionesFiltradas.forEach(t => {
    if (t.centroCosto) {
      centrosDeCosto.add(t.centroCosto);
      if (!resultadosPorCentro[t.centroCosto]) {
        resultadosPorCentro[t.centroCosto] = {
          ingresos: 0,
          gastos: 0,
          transacciones: []
        };
      }
    }
    t.partidas.forEach(p => {
      const cuentaStr = p.cuenta.toString();
      if (cuentaStr.startsWith('4')) {
        if (p.tipo === 'CR') {
          totalIngresos += p.monto;
          if (t.centroCosto) {
            resultadosPorCentro[t.centroCosto].ingresos += p.monto;
          }
        }
      } else if (cuentaStr.startsWith('6')) {
        if (p.tipo === 'DB') {
          totalGastos += p.monto;
          if (t.centroCosto) {
            resultadosPorCentro[t.centroCosto].gastos += p.monto;
          }
        }
      }
      const detalleTransaccion = {
        fecha: t.fecha,
        descripcion: t.descripcion,
        cuenta: p.cuenta,
        monto: p.monto,
        tipo: p.tipo,
        centroCosto: getCentroNombre(t.centroCosto)
      };
      detalleTransacciones.push(detalleTransaccion);
      if (t.centroCosto) {
        resultadosPorCentro[t.centroCosto].transacciones.push(detalleTransaccion);
      }
    });
  });
  let reporteHTML = `
    <div class="card">
      <div class="card-body">
        <div class="row mb-4">
          <div class="col">
            <div class="d-flex align-items-center">
              ${parametros.logo ? `<img src="${parametros.logo}" style="max-height: 100px; margin-right: 20px;">` : ''}
              <div>
                <h3>${parametros.nombre || 'Oratorio Virgen de Fátima'}</h3>
                ${parametros.direccion ? `<p>${parametros.direccion}</p>` : ''}
                ${parametros.telefono ? `<p>Tel: ${parametros.telefono}</p>` : ''}
                ${parametros.email ? `<p>Email: ${parametros.email}</p>` : ''}
              </div>
            </div>
          </div>
        </div>
        <h4>Reporte por Centro de Costo: ${centroCosto ? getCentroNombre(centroCosto) : 'Todos los Centros'}</h4>
        <h6>Período: ${desde} al ${hasta}</h6>
        <h5 class="mt-4">Resumen por Centro de Costo</h5>
        <table class="table">
          <thead>
            <tr>
              <th>Centro de Costo</th>
              <th>Ingresos</th>
              <th>Gastos</th>
              <th>Resultado</th>
            </tr>
          </thead>
          <tbody>
  `;
  centrosDeCosto.forEach(centro => {
    const resultado = resultadosPorCentro[centro];
    reporteHTML += `
      <tr>
        <td>${getCentroNombre(centro)}</td>
        <td>${resultado.ingresos.toFixed(2)}</td>
        <td>${resultado.gastos.toFixed(2)}</td>
        <td>${(resultado.ingresos - resultado.gastos).toFixed(2)}</td>
      </tr>
    `;
  });
  reporteHTML += `
        <tr class="table-secondary">
          <th>Total General</th>
          <th>${totalIngresos.toFixed(2)}</th>
          <th>${totalGastos.toFixed(2)}</th>
          <th>${(totalIngresos - totalGastos).toFixed(2)}</th>
        </tr>
      </tbody>
      </table>

      <div class="row mt-5">
        <div class="col-md-6 text-start">
          <hr style="width: 75%; margin: 0;">
          ${parametros.coordinador ? `<p>${parametros.coordinador}</p>` : ''}
          <p>Coordinador Responsable</p>
        </div>
        <div class="col-md-6 text-end">
          <hr style="width: 75%; margin: 0 0 0 auto;">
          ${parametros.tesorero ? `<p>${parametros.tesorero}</p>` : ''}
          <p>Tesorero</p>
        </div>
      </div>
    </div>
  </div>
  `;
  document.getElementById('reporteContent').innerHTML = reporteHTML;
  setTimeout(() => {
    window.print();
  }, 500);
}
function cerrarMes() {
  const mesCierre = document.getElementById('mesCierre').value;
  if (!mesCierre) {
    alert('Por favor seleccione el mes a cerrar');
    return;
  }
  const currentDate = new Date();
  const selectedDate = new Date(mesCierre);
  const minDate = new Date();
  minDate.setFullYear(currentDate.getFullYear() - 1);
  const maxDate = new Date();
  maxDate.setFullYear(currentDate.getFullYear() + 10);
  if (selectedDate < minDate || selectedDate > maxDate) {
    alert('La fecha seleccionada debe estar entre un año atrás y 10 años adelante');
    return;
  }
  const [year, month] = mesCierre.split('-');
  const firstDay = `${year}-${month}-01`;
  const lastDay = new Date(year, parseInt(month), 0).toISOString().split('T')[0];
  const transacciones = JSON.parse(localStorage.getItem('transacciones') || '[]');
  const transaccionesMes = transacciones.filter(t => {
    const fecha = new Date(t.fecha);
    return fecha >= new Date(firstDay) && fecha <= new Date(lastDay);
  });
  let saldoMes = 0;
  transaccionesMes.forEach(t => {
    t.partidas.forEach(p => {
      if (p.cuenta === '4.01.01') {
        if (p.tipo === 'CR') {
          saldoMes += p.monto;
        } else {
          saldoMes -= p.monto;
        }
      }
    });
  });
  mostrarDistribucionSaldo(saldoMes, mesCierre, year, month);
}
function mostrarDistribucionSaldo(saldoMes, mesCierre, year, month) {
  const centros = JSON.parse(localStorage.getItem('centros') || '[]');
  const tbody = document.querySelector('#distribucionTable tbody');
  tbody.innerHTML = '';
  document.getElementById('saldoTotalDistribuir').textContent = Math.abs(saldoMes).toFixed(2);
  centros.forEach(centro => {
    const tr = document.createElement('tr');
    tr.innerHTML = `
      <td>${centro.codigo} - ${centro.nombre}</td>
      <td>
        <input type="number" class="form-control distribution-amount" 
               data-centro="${centro.codigo}"
               step="0.01" min="0" max="${Math.abs(saldoMes)}"
               onchange="actualizarTotalDistribuido()">
      </td>
    `;
    tbody.appendChild(tr);
  });
  window.distribucionData = {
    saldoMes,
    mesCierre,
    year,
    month
  };
  const modal = new bootstrap.Modal(document.getElementById('distribucionSaldo'));
  modal.show();
}
function actualizarTotalDistribuido() {
  const inputs = document.querySelectorAll('.distribution-amount');
  let total = 0;
  inputs.forEach(input => {
    total += parseFloat(input.value || 0);
  });
  document.getElementById('totalDistribuido').textContent = total.toFixed(2);
}
function confirmarDistribucion() {
  const {
    saldoMes,
    mesCierre,
    year,
    month
  } = window.distribucionData;
  const inputs = document.querySelectorAll('.distribution-amount');
  let totalDistribuido = 0;
  const distribuciones = [];
  inputs.forEach(input => {
    const monto = parseFloat(input.value || 0);
    if (monto > 0) {
      totalDistribuido += monto;
      distribuciones.push({
        centroCosto: input.dataset.centro,
        monto: monto
      });
    }
  });
  if (Math.abs(totalDistribuido - Math.abs(saldoMes)) > 0.01) {
    alert('El total distribuido debe ser igual al saldo del mes');
    return;
  }
  const transacciones = JSON.parse(localStorage.getItem('transacciones') || '[]');
  const fechaCierre = new Date(year, parseInt(month) - 1, 31).toISOString().split('T')[0];
  const nextMonth = new Date(year, parseInt(month), 1);
  distribuciones.forEach(dist => {
    const transaccionCierre = {
      fecha: fechaCierre,
      tipoDocumento: 'CIERRE',
      descripcion: `Cierre del mes ${mesCierre} - Centro ${dist.centroCosto}`,
      monto: dist.monto,
      centroCosto: dist.centroCosto,
      partidas: [{
        cuenta: '1.01.01',
        tipo: 'CR',
        monto: dist.monto,
        centroCosto: dist.centroCosto
      }, {
        cuenta: '4.01.02',
        tipo: 'DB',
        monto: dist.monto,
        centroCosto: dist.centroCosto
      }],
      fechaCreacion: new Date().toISOString(),
      esCierre: true
    };
    const transaccionApertura = {
      fecha: nextMonth.toISOString().split('T')[0],
      tipoDocumento: 'APERTURA',
      descripcion: `Saldo inicial ${nextMonth.toISOString().split('-').slice(0, 2).join('-')} - Centro ${dist.centroCosto}`,
      monto: dist.monto,
      centroCosto: dist.centroCosto,
      partidas: [{
        cuenta: '1.01.01',
        tipo: 'DB',
        monto: dist.monto,
        centroCosto: dist.centroCosto
      }, {
        cuenta: '4.01.02',
        tipo: 'CR',
        monto: dist.monto,
        centroCosto: dist.centroCosto
      }],
      fechaCreacion: new Date().toISOString(),
      esApertura: true
    };
    transacciones.push(transaccionCierre, transaccionApertura);
  });
  localStorage.setItem('transacciones', JSON.stringify(transacciones));
  actualizarTablaTransacciones();
  const modal = bootstrap.Modal.getInstance(document.getElementById('distribucionSaldo'));
  modal.hide();
  alert('Mes cerrado exitosamente');
}
function guardarParametros() {
  const existingParams = JSON.parse(localStorage.getItem('parametrosBackup') || '{}');
  const logoInput = document.getElementById('logoOratorio');
  const file = logoInput.files[0];
  if (file) {
    const reader = new FileReader();
    reader.onload = function (e) {
      const parametros = {
        ...existingParams,
        nombre: document.getElementById('nombreOratorio').value,
        direccion: document.getElementById('direccionOratorio').value,
        telefono: document.getElementById('telefonoOratorio').value,
        email: document.getElementById('emailOratorio').value,
        coordinador: document.getElementById('coordinadorOratorio').value,
        tesorero: document.getElementById('tesoreroOratorio').value,
        logo: e.target.result || existingParams.logo
      };
      localStorage.setItem('parametrosOratorio', JSON.stringify(parametros));
      alert('Parámetros guardados exitosamente');
      document.getElementById('oratorioNombre').textContent = 'SISTEMA CONTABLE';
    };
    reader.readAsDataURL(file);
  } else {
    const parametros = {
      ...existingParams,
      nombre: document.getElementById('nombreOratorio').value,
      direccion: document.getElementById('direccionOratorio').value,
      telefono: document.getElementById('telefonoOratorio').value,
      email: document.getElementById('emailOratorio').value,
      coordinador: document.getElementById('coordinadorOratorio').value,
      tesorero: document.getElementById('tesoreroOratorio').value,
      logo: document.getElementById('logoPreview').querySelector('img')?.src || existingParams.logo
    };
    localStorage.setItem('parametrosOratorio', JSON.stringify(parametros));
    alert('Parámetros guardados exitosamente');
    document.getElementById('oratorioNombre').textContent = 'SISTEMA CONTABLE';
  }
}
function cargarParametros() {
  const parametrosBackup = JSON.parse(localStorage.getItem('parametrosBackup') || '{}');
  const parametros = {
    ...JSON.parse(localStorage.getItem('parametrosOratorio') || '{}'),
    ...parametrosBackup
  };
  document.getElementById('nombreOratorio').value = parametros.nombre || '';
  document.getElementById('direccionOratorio').value = parametros.direccion || '';
  document.getElementById('telefonoOratorio').value = parametros.telefono || '';
  document.getElementById('emailOratorio').value = parametros.email || '';
  document.getElementById('coordinadorOratorio').value = parametros.coordinador || '';
  document.getElementById('tesoreroOratorio').value = parametros.tesorero || '';
  document.getElementById('oratorioNombre').textContent = 'SISTEMA CONTABLE';
  const logoPreview = document.getElementById('logoPreview');
  if (parametros.logo) {
    logoPreview.innerHTML = `<img src="${parametros.logo}" style="max-height: 100px;" class="img-fluid">`;
  } else {
    logoPreview.innerHTML = '';
  }
}
function migrateDataToLocalStorage() {
  if (localStorage.getItem('dataMigrated')) {
    return;
  }
  const cuentasExistentes = JSON.parse(localStorage.getItem('cuentas') || '[]');
  if (cuentasExistentes.length > 0) {
    localStorage.setItem('cuentasBackup', JSON.stringify(cuentasExistentes));
  }
  const documentosExistentes = JSON.parse(localStorage.getItem('documentos') || '[]');
  if (documentosExistentes.length > 0) {
    localStorage.setItem('documentosBackup', JSON.stringify(documentosExistentes));
  }
  const centrosExistentes = JSON.parse(localStorage.getItem('centros') || '[]');
  if (centrosExistentes.length > 0) {
    localStorage.setItem('centrosBackup', JSON.stringify(centrosExistentes));
  }
  const transaccionesExistentes = JSON.parse(localStorage.getItem('transacciones') || '[]');
  if (transaccionesExistentes.length > 0) {
    localStorage.setItem('transaccionesBackup', JSON.stringify(transaccionesExistentes));
  }
  const parametrosExistentes = JSON.parse(localStorage.getItem('parametrosOratorio') || '{}');
  if (Object.keys(parametrosExistentes).length > 0) {
    localStorage.setItem('parametrosBackup', JSON.stringify(parametrosExistentes));
  }
  localStorage.setItem('dataMigrated', 'true');
}
function logout() {
  currentUser = null;
  document.getElementById('loginContainer').style.display = 'block';
  document.querySelector('.container-fluid').style.display = 'none';
  document.getElementById('loginForm').reset();
}
function nuevaPartidaManual() {
  const fecha = document.getElementById('fechaPartidaManual').value;
  const descripcion = document.getElementById('descripcionPartidaManual').value;
  if (!fecha || !descripcion) {
    alert('Por favor complete la fecha y descripción');
    return;
  }
  document.getElementById('lineasPartida').innerHTML = '';
  document.getElementById('totalDebito').textContent = '0.00';
  document.getElementById('totalCredito').textContent = '0.00';
  agregarLineaPartida();
  window.partidaManualTemp = {
    fecha,
    descripcion
  };
  const modal = new bootstrap.Modal(document.getElementById('partidaManualModal'));
  modal.show();
}
function agregarLineaPartida() {
  const container = document.getElementById('lineasPartida');
  const lineNum = container.children.length + 1;
  const div = document.createElement('div');
  div.className = 'row mb-2 partida-line';
  const cuentas = JSON.parse(localStorage.getItem('cuentas') || '[]');
  const centros = JSON.parse(localStorage.getItem('centros') || '[]');
  div.innerHTML = `
    <div class="col-md-4">
      <select class="form-select cuenta-select" onchange="actualizarTotalesPartida()">
        <option value="">Seleccione cuenta...</option>
        ${cuentas.map(c => `<option value="${c.codigo}">${c.codigo} - ${c.nombre}</option>`).join('')}
      </select>
    </div>
    <div class="col-md-2">
      <select class="form-select tipo-select" onchange="actualizarTotalesPartida()">
        <option value="DB">Débito</option>
        <option value="CR">Crédito</option>
      </select>
    </div>
    <div class="col-md-3">
      <input type="number" class="form-control monto-input" 
             step="0.01" min="0" onchange="actualizarTotalesPartida()">
    </div>
    <div class="col-md-3">
      <select class="form-select centro-select">
        <option value="">Sin centro de costo</option>
        ${centros.map(c => `<option value="${c.codigo}">${c.codigo} - ${c.nombre}</option>`).join('')}
      </select>
    </div>
  `;
  container.appendChild(div);
}
function actualizarTotalesPartida() {
  let totalDB = 0;
  let totalCR = 0;
  document.querySelectorAll('.partida-line').forEach(line => {
    const monto = parseFloat(line.querySelector('.monto-input').value) || 0;
    const tipo = line.querySelector('.tipo-select').value;
    if (tipo === 'DB') {
      totalDB += monto;
    } else {
      totalCR += monto;
    }
  });
  document.getElementById('totalDebito').textContent = totalDB.toFixed(2);
  document.getElementById('totalCredito').textContent = totalCR.toFixed(2);
}
function guardarPartidaManual() {
  const {
    fecha,
    descripcion
  } = window.partidaManualTemp;
  const partidas = [];
  let totalDB = 0;
  let totalCR = 0;
  document.querySelectorAll('.partida-line').forEach(line => {
    const cuenta = line.querySelector('.cuenta-select').value;
    const tipo = line.querySelector('.tipo-select').value;
    const monto = parseFloat(line.querySelector('.monto-input').value) || 0;
    const centroCosto = line.querySelector('.centro-select').value;
    if (!cuenta || !monto) return;
    if (tipo === 'DB') totalDB += monto;else totalCR += monto;
    partidas.push({
      cuenta,
      tipo,
      monto,
      centroCosto
    });
  });
  if (Math.abs(totalDB - totalCR) > 0.01) {
    alert('Los totales débito y crédito deben ser iguales');
    return;
  }
  if (partidas.length < 2) {
    alert('Debe ingresar al menos dos líneas');
    return;
  }
  const transaccion = {
    fecha,
    tipoDocumento: 'MANUAL',
    descripcion,
    monto: totalDB,
    partidas,
    fechaCreacion: new Date().toISOString()
  };
  let transacciones = JSON.parse(localStorage.getItem('transacciones') || '[]');
  transacciones.push(transaccion);
  localStorage.setItem('transacciones', JSON.stringify(transacciones));
  const modal = bootstrap.Modal.getInstance(document.getElementById('partidaManualModal'));
  modal.hide();
  document.getElementById('fechaPartidaManual').value = '';
  document.getElementById('descripcionPartidaManual').value = '';
  actualizarTablaTransacciones();
  alert('Partida manual guardada exitosamente');
}
function showModal(modalId) {
  const modal = new bootstrap.Modal(document.getElementById(modalId));
  if (modalId === 'nuevoDocumento') {
    populateCuentaSelects();
  }
  if (modalId === 'nuevaTransaccion') {
    populateDocumentTypes();
    const centros = JSON.parse(localStorage.getItem('centros') || '[]');
    const select = document.getElementById('centroCostoTransaccion');
    select.innerHTML = '<option value="">-- Ninguno --</option>';
    centros.forEach(centro => {
      const option = document.createElement('option');
      option.value = centro.codigo;
      option.textContent = `${centro.codigo} - ${centro.nombre}`;
      select.appendChild(option);
    });
  }
  if (modalId === 'nuevaCuenta') {
    const centros = JSON.parse(localStorage.getItem('centros') || '[]');
    const select = document.getElementById('centroCostoSelect');
    select.innerHTML = '<option value="">-- Ninguno --</option>';
    centros.forEach(centro => {
      const option = document.createElement('option');
      option.value = centro.codigo;
      option.textContent = `${centro.codigo} - ${centro.nombre}`;
      select.appendChild(option);
    });
  }
  modal.show();
}
function actualizarTablaDocumentos() {
  const documentosBackup = JSON.parse(localStorage.getItem('documentosBackup') || '[]');
  const documentos = [...JSON.parse(localStorage.getItem('documentos') || '[]')];
  documentos.push(...documentosBackup.filter(d => !documentos.find(ed => ed.codigo === d.codigo)));
  const tbody = document.querySelector('#documentos table tbody');
  tbody.innerHTML = documentos.map(doc => `
    <tr>
      <td>${doc.codigo}</td>
      <td>${doc.nombre}</td>
      <td>
        ${doc.partidas.map(p => `
          <div>${p.cuenta} - ${p.tipo}</div>
        `).join('')}
      </td>
      <td>
        <button class="btn btn-sm btn-info">
          <i class="fas fa-edit"></i>
        </button>
        <button class="btn btn-sm btn-danger" onclick="eliminarDocumento('${doc.codigo}')">
          <i class="fas fa-trash"></i>
        </button>
      </td>
    </tr>
  `).join('');
}
function eliminarDocumento(codigo) {
  if (confirm('¿Está seguro de eliminar este tipo de documento?')) {
    let documentos = JSON.parse(localStorage.getItem('documentos') || '[]');
    documentos = documentos.filter(d => d.codigo !== codigo);
    localStorage.setItem('documentos', JSON.stringify(documentos));
    actualizarTablaDocumentos();
  }
}
function generarLibroDiario() {
  const desde = document.getElementById('libroDiarioDesde').value;
  const hasta = document.getElementById('libroDiarioHasta').value;
  if (!desde || !hasta) {
    alert('Por favor complete las fechas');
    return;
  }
  const parametros = JSON.parse(localStorage.getItem('parametrosOratorio') || '{}');
  const transacciones = JSON.parse(localStorage.getItem('transacciones') || '[]').filter(t => {
    const fecha = new Date(t.fecha);
    return fecha >= new Date(desde) && fecha <= new Date(hasta);
  }).sort((a, b) => new Date(a.fecha) - new Date(b.fecha));
  let reporteHTML = `
    <div class="card">
      <div class="card-body">
        <div class="row mb-4">
          <div class="col">
            <div class="d-flex align-items-center">
              ${parametros.logo ? `<img src="${parametros.logo}" style="max-height: 100px; margin-right: 20px;">` : ''}
              <div>
                <h3>${parametros.nombre || 'Oratorio Virgen de Fátima'}</h3>
                ${parametros.direccion ? `<p>${parametros.direccion}</p>` : ''}
                ${parametros.telefono ? `<p>Tel: ${parametros.telefono}</p>` : ''}
                ${parametros.email ? `<p>Email: ${parametros.email}</p>` : ''}
              </div>
            </div>
          </div>
        </div>

        <h4>Libro Diario</h4>
        <h6>Período: ${desde} al ${hasta}</h6>

        <table class="table">
          <thead>
            <tr>
              <th>Fecha</th>
              <th>Documento</th>
              <th>Descripción</th>
              <th>Cuenta</th>
              <th>Débito</th>
              <th>Crédito</th>
            </tr>
          </thead>
          <tbody>
  `;
  let totalDB = 0;
  let totalCR = 0;
  transacciones.forEach(t => {
    reporteHTML += `
      <tr class="table-secondary">
        <td colspan="6"><strong>${t.fecha} - ${t.descripcion}</strong></td>
      </tr>
    `;
    t.partidas.forEach(p => {
      if (p.tipo === 'DB') totalDB += p.monto;
      if (p.tipo === 'CR') totalCR += p.monto;
      reporteHTML += `
        <tr>
          <td></td>
          <td>${t.tipoDocumento}</td>
          <td>${p.centroCosto ? `CC: ${p.centroCosto}` : ''}</td>
          <td>${p.cuenta}</td>
          <td>${p.tipo === 'DB' ? p.monto.toFixed(2) : ''}</td>
          <td>${p.tipo === 'CR' ? p.monto.toFixed(2) : ''}</td>
        </tr>
      `;
    });
  });
  reporteHTML += `
          <tr class="table-secondary">
            <th colspan="4">Totales</th>
            <th>${totalDB.toFixed(2)}</th>
            <th>${totalCR.toFixed(2)}</th>
          </tr>
          </tbody>
        </table>

        <div class="row mt-5">
          <div class="col-md-6 text-start">
            <hr style="width: 75%; margin: 0;">
            ${parametros.coordinador ? `<p>${parametros.coordinador}</p>` : ''}
            <p>Coordinador Responsable</p>
          </div>
          <div class="col-md-6 text-end">
            <hr style="width: 75%; margin: 0 0 0 auto;">
            ${parametros.tesorero ? `<p>${parametros.tesorero}</p>` : ''}
            <p>Tesorero</p>
          </div>
        </div>
      </div>
    </div>
  `;
  document.getElementById('reporteContent').innerHTML = reporteHTML;
  setTimeout(() => {
    window.print();
  }, 500);
}
function generarIngresosGastos() {
  const desde = document.getElementById('ingresosGastosDesde').value;
  const hasta = document.getElementById('ingresosGastosHasta').value;
  if (!desde || !hasta) {
    alert('Por favor complete las fechas');
    return;
  }
  const parametros = JSON.parse(localStorage.getItem('parametrosOratorio') || '{}');
  const transacciones = JSON.parse(localStorage.getItem('transacciones') || '[]').filter(t => {
    const fecha = new Date(t.fecha);
    return fecha >= new Date(desde) && fecha <= new Date(hasta);
  });
  let saldoInicial = 0;
  let totalIngresos = 0;
  let totalGastos = 0;
  transacciones.forEach(t => {
    t.partidas.forEach(p => {
      const cuentaStr = p.cuenta.toString();
      if (cuentaStr === '4.01.02' && p.tipo === 'CR') {
        saldoInicial += p.monto;
      } else if (cuentaStr.startsWith('4') && cuentaStr !== '4.01.02') {
        if (p.tipo === 'CR') totalIngresos += p.monto;
        if (p.tipo === 'DB') totalIngresos -= p.monto;
      } else if (cuentaStr.startsWith('6')) {
        if (p.tipo === 'DB') totalGastos += p.monto;
        if (p.tipo === 'CR') totalGastos -= p.monto;
      }
    });
  });
  const saldoDisponible = saldoInicial + totalIngresos - totalGastos;
  let reporteHTML = `
    <div class="card">
      <div class="card-body">
        <div class="row mb-4">
          <div class="col">
            <div class="d-flex align-items-center">
              ${parametros.logo ? `<img src="${parametros.logo}" style="max-height: 100px; margin-right: 20px;">` : ''}
              <div>
                <h3>${parametros.nombre || 'Oratorio Virgen de Fátima'}</h3>
                ${parametros.direccion ? `<p>${parametros.direccion}</p>` : ''}
                ${parametros.telefono ? `<p>Tel: ${parametros.telefono}</p>` : ''}
                ${parametros.email ? `<p>Email: ${parametros.email}</p>` : ''}
              </div>
            </div>
          </div>
        </div>

        <h4>Estado de Ingresos y Gastos</h4>
        <h6>Período: ${desde} al ${hasta}</h6>

        <table class="table mt-4">
          <tbody>
            <tr>
              <td colspan="2"><strong>Saldo Acumulado del mes Anterior</strong></td>
              <td class="text-end">${saldoInicial.toFixed(2)}</td>
            </tr>
            <tr>
              <td colspan="2"><strong>Ingresos del Período</strong></td>
              <td class="text-end">${totalIngresos.toFixed(2)}</td>
            </tr>
            <tr>
              <td colspan="2"><strong>Menos: Gastos del Período</strong></td>
              <td class="text-end">${totalGastos.toFixed(2)}</td>
            </tr>
            <tr class="table-secondary">
              <td colspan="2"><strong>Saldo Disponible en Caja</strong></td>
              <td class="text-end"><strong>${saldoDisponible.toFixed(2)}</strong></td>
            </tr>
          </tbody>
        </table>

        <div class="row mt-5">
          <div class="col-md-6 text-start">
            <hr style="width: 75%; margin: 0;">
            ${parametros.coordinador ? `<p>${parametros.coordinador}</p>` : ''}
            <p>Coordinador Responsable</p>
          </div>
          <div class="col-md-6 text-end">
            <hr style="width: 75%; margin: 0 0 0 auto;">
            ${parametros.tesorero ? `<p>${parametros.tesorero}</p>` : ''}
            <p>Tesorero</p>
          </div>
        </div>

      </div>
    </div>
  `;
  document.getElementById('reporteContent').innerHTML = reporteHTML;
  setTimeout(() => {
    window.print();
  }, 500);
}
function generarBalanceGeneral() {
  const fecha = document.getElementById('fechaBalance').value;
  if (!fecha) {
    alert('Por favor seleccione una fecha');
    return;
  }
  const parametros = JSON.parse(localStorage.getItem('parametrosOratorio') || '{}');
  const transacciones = JSON.parse(localStorage.getItem('transacciones') || '[]').filter(t => new Date(t.fecha) <= new Date(fecha));
  const saldos = {};
  transacciones.forEach(t => {
    t.partidas.forEach(p => {
      if (!saldos[p.cuenta]) {
        saldos[p.cuenta] = 0;
      }
      if (p.tipo === 'DB') {
        saldos[p.cuenta] += p.monto;
      } else {
        saldos[p.cuenta] -= p.monto;
      }
    });
  });
  const cuentas = JSON.parse(localStorage.getItem('cuentas') || '[]');
  const activos = [];
  const pasivos = [];
  const capital = [];
  let totalActivos = 0;
  let totalPasivos = 0;
  let totalCapital = 0;
  Object.entries(saldos).forEach(([codigo, saldo]) => {
    const cuenta = cuentas.find(c => c.codigo === codigo);
    if (!cuenta) return;
    const saldoAjustado = cuenta.tipo === 'pasivo' || cuenta.tipo === 'capital' ? -saldo : saldo;
    if (cuenta.tipo === 'activo') {
      activos.push({
        ...cuenta,
        saldo: saldoAjustado
      });
      totalActivos += saldoAjustado;
    } else if (cuenta.tipo === 'pasivo') {
      pasivos.push({
        ...cuenta,
        saldo: saldoAjustado
      });
      totalPasivos += saldoAjustado;
    } else if (cuenta.tipo === 'capital') {
      capital.push({
        ...cuenta,
        saldo: saldoAjustado
      });
      totalCapital += saldoAjustado;
    }
  });
  let reporteHTML = `
    <div class="card">
      <div class="card-body">
        <div class="row mb-4">
          <div class="col">
            <div class="d-flex align-items-center">
              ${parametros.logo ? `<img src="${parametros.logo}" style="max-height: 100px; margin-right: 20px;">` : ''}
              <div>
                <h3>${parametros.nombre || 'Oratorio Virgen de Fátima'}</h3>
                ${parametros.direccion ? `<p>${parametros.direccion}</p>` : ''}
                ${parametros.telefono ? `<p>Tel: ${parametros.telefono}</p>` : ''}
                ${parametros.email ? `<p>Email: ${parametros.email}</p>` : ''}
              </div>
            </div>
          </div>
        </div>

        <h4>Balance General</h4>
        <h6>Al ${new Date(fecha).toLocaleDateString()}</h6>

        <div class="row mt-4">
          <div class="col-md-6">
            <h5>ACTIVOS</h5>
            <table class="table">
              <tbody>
                ${activos.map(cuenta => `
                  <tr>
                    <td>${cuenta.codigo} - ${cuenta.nombre}</td>
                    <td class="text-end">${Math.abs(cuenta.saldo).toFixed(2)}</td>
                  </tr>
                `).join('')}
                <tr class="table-secondary">
                  <th>Total Activos</th>
                  <th class="text-end">${Math.abs(totalActivos).toFixed(2)}</th>
                </tr>
              </tbody>
            </table>
          </div>

          <div class="col-md-6">
            <h5>PASIVOS</h5>
            <table class="table">
              <tbody>
                ${pasivos.map(cuenta => `
                  <tr>
                    <td>${cuenta.codigo} - ${cuenta.nombre}</td>
                    <td class="text-end">${Math.abs(cuenta.saldo).toFixed(2)}</td>
                  </tr>
                `).join('')}
                <tr class="table-secondary">
                  <th>Total Pasivos</th>
                  <th class="text-end">${Math.abs(totalPasivos).toFixed(2)}</th>
                </tr>
              </tbody>
            </table>

            <h5 class="mt-4">PATRIMONIO</h5>
            <table class="table">
              <tbody>
                ${capital.map(cuenta => `
                  <tr>
                    <td>${cuenta.codigo} - ${cuenta.nombre}</td>
                    <td class="text-end">${Math.abs(cuenta.saldo).toFixed(2)}</td>
                  </tr>
                `).join('')}
                <tr class="table-secondary">
                  <th>Total Patrimonio</th>
                  <th class="text-end">${Math.abs(totalCapital).toFixed(2)}</th>
                </tr>
              </tbody>
            </table>

            <table class="table mt-4">
              <tbody>
                <tr class="table-secondary">
                  <th>TOTAL PASIVO Y PATRIMONIO</th>
                  <th class="text-end">${Math.abs(totalPasivos + totalCapital).toFixed(2)}</th>
                </tr>
              </tbody>
            </table>
          </div>
        </div>

        <div class="row mt-5">
          <div class="col-md-6 text-start">
            <hr style="width: 75%; margin: 0;">
            ${parametros.coordinador ? `<p>${parametros.coordinador}</p>` : ''}
            <p>Coordinador Responsable</p>
          </div>
          <div class="col-md-6 text-end">
            <hr style="width: 75%; margin: 0 0 0 auto;">
            ${parametros.tesorero ? `<p>${parametros.tesorero}</p>` : ''}
            <p>Tesorero</p>
          </div>
        </div>

      </div>
    </div>
  `;
  document.getElementById('reporteContent').innerHTML = reporteHTML;
  setTimeout(() => {
    window.print();
  }, 500);
}
function generarLibroMayor() {
  const cuenta = document.getElementById('libroMayorCuenta').value;
  const desde = document.getElementById('libroMayorDesde').value;
  const hasta = document.getElementById('libroMayorHasta').value;
  if (!cuenta || !desde || !hasta) {
    alert('Por favor complete todos los campos');
    return;
  }
  const parametros = JSON.parse(localStorage.getItem('parametrosOratorio') || '{}');
  const transacciones = JSON.parse(localStorage.getItem('transacciones') || '[]').filter(t => {
    const fecha = new Date(t.fecha);
    return fecha >= new Date(desde) && fecha <= new Date(hasta);
  }).sort((a, b) => new Date(a.fecha) - new Date(b.fecha));
  const cuentas = JSON.parse(localStorage.getItem('cuentas') || '[]');
  const cuentaInfo = cuentas.find(c => c.codigo === cuenta);
  if (!cuentaInfo) {
    alert('Cuenta no encontrada');
    return;
  }
  let saldoAcumulado = 0;
  const movimientos = [];
  transacciones.forEach(t => {
    t.partidas.forEach(p => {
      if (p.cuenta === cuenta) {
        const monto = p.tipo === 'DB' ? p.monto : -p.monto;
        saldoAcumulado += monto;
        movimientos.push({
          fecha: t.fecha,
          documento: t.tipoDocumento,
          descripcion: t.descripcion,
          debe: p.tipo === 'DB' ? p.monto : 0,
          haber: p.tipo === 'CR' ? p.monto : 0,
          saldo: saldoAcumulado
        });
      }
    });
  });
  let reporteHTML = `
    <div class="card">
      <div class="card-body">
        <div class="row mb-4">
          <div class="col">
            <div class="d-flex align-items-center">
              ${parametros.logo ? `<img src="${parametros.logo}" style="max-height: 100px; margin-right: 20px;">` : ''}
              <div>
                <h3>${parametros.nombre || 'Oratorio Virgen de Fátima'}</h3>
                ${parametros.direccion ? `<p>${parametros.direccion}</p>` : ''}
                ${parametros.telefono ? `<p>Tel: ${parametros.telefono}</p>` : ''}
                ${parametros.email ? `<p>Email: ${parametros.email}</p>` : ''}
              </div>
            </div>
          </div>
        </div>

        <h4>Libro Mayor</h4>
        <h5>Cuenta: ${cuenta} - ${cuentaInfo.nombre}</h5>
        <h6>Período: ${desde} al ${hasta}</h6>

        <table class="table mt-4">
          <thead>
            <tr>
              <th>Fecha</th>
              <th>Documento</th>
              <th>Descripción</th>
              <th>Debe</th>
              <th>Haber</th>
              <th>Saldo</th>
            </tr>
          </thead>
          <tbody>
            ${movimientos.map(m => `
              <tr>
                <td>${m.fecha}</td>
                <td>${m.documento}</td>
                <td>${m.descripcion}</td>
                <td>${m.debe.toFixed(2)}</td>
                <td>${m.haber.toFixed(2)}</td>
                <td>${m.saldo.toFixed(2)}</td>
              </tr>
            `).join('')}
          </tbody>
          <tfoot>
            <tr class="table-secondary">
              <th colspan="3">Totales</th>
              <th>${movimientos.reduce((sum, m) => sum + m.debe, 0).toFixed(2)}</th>
              <th>${movimientos.reduce((sum, m) => sum + m.haber, 0).toFixed(2)}</th>
              <th>${saldoAcumulado.toFixed(2)}</th>
            </tr>
          </tfoot>
        </table>

        <div class="row mt-5">
          <div class="col-md-6 text-start">
            <hr style="width: 75%; margin: 0;">
            ${parametros.coordinador ? `<p>${parametros.coordinador}</p>` : ''}
            <p>Coordinador Responsable</p>
          </div>
          <div class="col-md-6 text-end">
            <hr style="width: 75%; margin: 0 0 0 auto;">
            ${parametros.tesorero ? `<p>${parametros.tesorero}</p>` : ''}
            <p>Tesorero</p>
          </div>
        </div>

      </div>
    </div>
  `;
  document.getElementById('reporteContent').innerHTML = reporteHTML;
  setTimeout(() => {
    window.print();
  }, 500);
}
function crearBackup() {
  const backup = {
    cuentas: JSON.parse(localStorage.getItem('cuentas') || '[]'),
    documentos: JSON.parse(localStorage.getItem('documentos') || '[]'),
    centros: JSON.parse(localStorage.getItem('centros') || '[]'),
    transacciones: JSON.parse(localStorage.getItem('transacciones') || '[]'),
    parametros: JSON.parse(localStorage.getItem('parametrosOratorio') || '{}'),
    timestamp: new Date().toISOString()
  };
  const blob = new Blob([JSON.stringify(backup, null, 2)], {
    type: 'application/json'
  });
  const url = URL.createObjectURL(blob);
  const a = document.createElement('a');
  a.href = url;
  a.download = `backup_sistema_contable_${new Date().toISOString().split('T')[0]}.json`;
  document.body.appendChild(a);
  a.click();
  document.body.removeChild(a);
  URL.revokeObjectURL(url);
}
function restaurarBackup() {
  const fileInput = document.getElementById('backupFile');
  const file = fileInput.files[0];
  if (!file) {
    alert('Por favor seleccione un archivo de backup');
    return;
  }
  const reader = new FileReader();
  reader.onload = function (e) {
    try {
      const backup = JSON.parse(e.target.result);
      const requiredKeys = ['cuentas', 'documentos', 'centros', 'transacciones', 'parametros', 'timestamp'];
      const hasAllKeys = requiredKeys.every(key => backup.hasOwnProperty(key));
      if (!hasAllKeys) {
        throw new Error('Archivo de backup inválido');
      }
      localStorage.setItem('cuentasBackup', localStorage.getItem('cuentas') || '[]');
      localStorage.setItem('documentosBackup', localStorage.getItem('documentos') || '[]');
      localStorage.setItem('centrosBackup', localStorage.getItem('centros') || '[]');
      localStorage.setItem('transaccionesBackup', localStorage.getItem('transacciones') || '[]');
      localStorage.setItem('parametrosBackup', localStorage.getItem('parametrosOratorio') || '{}');
      localStorage.setItem('cuentas', JSON.stringify(backup.cuentas));
      localStorage.setItem('documentos', JSON.stringify(backup.documentos));
      localStorage.setItem('centros', JSON.stringify(backup.centros));
      localStorage.setItem('transacciones', JSON.stringify(backup.transacciones));
      localStorage.setItem('parametrosOratorio', JSON.stringify(backup.parametros));
      actualizarCatalogo();
      actualizarTablaDocumentos();
      actualizarTablaTransacciones();
      actualizarTablaCentros();
      cargarParametros();
      alert('Backup restaurado exitosamente');
      fileInput.value = '';
    } catch (error) {
      alert('Error al restaurar el backup: ' + error.message);
    }
  };
  reader.readAsText(file);
}
document.addEventListener('DOMContentLoaded', () => {
  migrateDataToLocalStorage();
  showSection('catalogo');
  cargarParametros();
  let cuentasPredefinidas = [{
    codigo: '1.01.01',
    nombre: 'Caja General',
    tipo: 'activo'
  }, {
    codigo: '4.01.01',
    nombre: 'Ingresos del mes',
    tipo: 'ingreso'
  }, {
    codigo: '4.01.02',
    nombre: 'Saldo del mes anterior',
    tipo: 'ingreso'
  }, {
    codigo: '6.01.01',
    nombre: 'Gastos del mes',
    tipo: 'gasto'
  }];
  let cuentasExistentes = JSON.parse(localStorage.getItem('cuentas') || '[]');
  cuentasPredefinidas.forEach(cuenta => {
    if (!cuentasExistentes.find(c => c.codigo === cuenta.codigo)) {
      cuentasExistentes.push({
        ...cuenta,
        fechaCreacion: new Date().toISOString()
      });
    }
  });
  localStorage.setItem('cuentas', JSON.stringify(cuentasExistentes));
  actualizarCatalogo();
  populateCuentaSelects();
  actualizarTablaDocumentos();
  actualizarTablaTransacciones();
  actualizarTablaCentros();
  document.querySelector('#nuevaCuenta .modal-footer .btn-primary').addEventListener('click', guardarCuenta);
  const centroCostoReporte = document.getElementById('centroCostoReporte');
  const centros = JSON.parse(localStorage.getItem('centros') || '[]');
  centroCostoReporte.innerHTML = '<option value="">-- Todos los Centros --</option>';
  centros.forEach(centro => {
    const option = document.createElement('option');
    option.value = centro.codigo;
    option.textContent = `${centro.codigo} - ${centro.nombre}`;
    centroCostoReporte.appendChild(option);
  });
  const mesCierreInput = document.getElementById('mesCierre');
  const currentDate = new Date();
  const minDate = new Date();
  minDate.setFullYear(currentDate.getFullYear() - 1);
  const maxDate = new Date();
  maxDate.setFullYear(currentDate.getFullYear() + 10);
  mesCierreInput.min = minDate.toISOString().slice(0, 7);
  mesCierreInput.max = maxDate.toISOString().slice(0, 7);
  const centroCostoCierre = document.getElementById('centroCostoCierre');
  const centrosCierre = JSON.parse(localStorage.getItem('centros') || '[]');
  centroCostoCierre.innerHTML = '<option value="">-- Ninguno --</option>';
  centrosCierre.forEach(centro => {
    const option = document.createElement('option');
    option.value = centro.codigo;
    option.textContent = `${centro.codigo} - ${centro.nombre}`;
    centroCostoCierre.appendChild(option);
  });
  document.getElementById('logoOratorio').addEventListener('change', function (e) {
    const file = e.target.files[0];
    if (file) {
      const reader = new FileReader();
      reader.onload = function (e) {
        const logoPreview = document.getElementById('logoPreview');
        logoPreview.innerHTML = `<img src="${e.target.result}" style="max-height: 100px;" class="img-fluid">`;
      };
      reader.readAsDataURL(file);
    }
  });
  const libroMayorSelect = document.getElementById('libroMayorCuenta');
  const cuentas = JSON.parse(localStorage.getItem('cuentas') || '[]');
  libroMayorSelect.innerHTML = '<option value="">-- Seleccione una cuenta --</option>';
  cuentas.forEach(cuenta => {
    const option = document.createElement('option');
    option.value = cuenta.codigo;
    option.textContent = `${cuenta.codigo} - ${cuenta.nombre}`;
    libroMayorSelect.appendChild(option);
  });
  document.querySelector('.container-fluid').style.display = 'none';
  document.getElementById('backupFile').addEventListener('change', function (e) {
    const file = e.target.files[0];
    if (file && !file.name.endsWith('.json')) {
      alert('Por favor seleccione un archivo JSON válido');
      this.value = '';
    }
  });
});</script>
</body>
</html>
